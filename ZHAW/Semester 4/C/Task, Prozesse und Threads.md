#c #sem4
## Multi-Tasking
### Task
Aufgabe, die von CPU abarbeitet wird.
### Batch-Ausführung
Anstehende Tasks werden hintereinander gestartet.
### Multi-Tasking
- Task nebeneinander laufen lassen
- zwischen Tasks wechseln
### Scheduling
- kooperativ: Task entscheidet über Kontrolle
- präemptiv: Kontrollübergabe wird erzwungen
- Scheduler: unterbricht Tasks präemptiv & entscheidet welcher der nächste ist
## Prozesse und Threads
### Prozess
ein Kontrollfluss, eigenes virtuelles Memory
- Kernel bietet ausgeführtem Maschinencode von Prozess Illusion, er habe alleinige Kontrolle über CPU & Speicher
- wird durch OS kontrolliert (Kontrollblock)
- Stati
	- running/active
	- ready
	- blocked
	- terminated
### Thread
Separater Kontrollfluss/Stack innerhalb von Prozess, teilt Memory mit Eltern-Prozess.
Somit keine Kosten beim Kontext Switch, Schutz ist allerdings nicht gegeben.
## Lebenszyklen
### Prozess
![[Pasted image 20240612200818.png#invert]]

Commands:
- fork(): dupliziert Elternprozess und fährt Code in beiden Prozessen hinter fork()-Aufruf weiter (Child erbt Ressourcen wie offene Files von Parent)
	- Return-Codes
		- -1: Fehler
		- 0: Child
		- >0: Parent, pid des Childs
	- execv(): Zusatz zu fork() wenn ein neues Programm als Child geladen werden soll
- exit(): terminiert Prozess, gibt Exit-Code an wait() von Parent weiter
- wait(): wartet bis Prozess terminiert
	- wenn wait() im Parent bevor Child terminiert ist Parent solange blockiert
	- wait() kommt erst, nachdem Child schon terminated => Child ist im terminated Zustand (Zombie)
	- wenn Parent terminiert obwohl Child noch läuft => Orphan. Normalerweise werden Childs an den nächsten Parent vererbt.
- waitpid(): nimmt Exitcode von Child entgegend (blocking or non-blocking)
- wexitstatus(): extrahiert Exitcode aus wait()
- system(): ruft Programm auf und wartet, bis es terminiert
- popen(): Convenience-Funktion zum Lesen von stdout der Programme (Abwandlung von system())

Allgemein:


Beispiel fork()

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
int main()
{
	pid_t cpid = fork();
	if (cpid == -1) PERROR_AND_EXIT("fork");
	if (cpid > 0) {
		// still in parent process
		printf("Parent: %d forked child %d\n", getpid(), cpid);
		int wstatus;
		pid_t wpid = waitpid(cpid, &wstatus, 0); // wait blocking for child to    terminate
		if (wpid == -1) PERROR_AND_EXIT("waitpid");
		printf("Parent: child %d exited with %d (status=0x%x)\n", cpid, WEXITSTATUS(wstatus), wstatus);
		exit(EXIT_SUCCESS);
	} else {
		// in child process
		printf("Child: %d forked by parent %d\n", getpid(), getppid());
		sleep(3);
		exit(123);
	}
}
```

Beispiel execv()
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
int main() {
	pid_t cpid = fork();
	if (cpid == -1) PERROR_AND_EXIT("fork");
	if (cpid > 0) {
		// still in parent process
		printf("Parent: %d forked child %d\n", getpid(), cpid);
		int wstatus;
		pid_t wpid = waitpid(cpid, &wstatus, 0); // wait blocking for child to terminate
		if (wpid == -1) PERROR_AND_EXIT("waitpid");
		printf("Parent: child %d exited with %d (status=0x%x)\n", cpid, WEXITSTATUS(wstatus), wstatus);
		exit(EXIT_SUCCESS);
	} else {
		// in child process: replace current image by new image
		static char *eargv[] = { "ls", "-l", NULL }; // argv of the execv image below
		if (execv("/bin/ls", eargv) == -1) PERROR_AND_EXIT("execv: /bin/ls");
		// this line is never reached
	}
}
```

Beispiel system()
```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
int main()
{
	int ret = system("/bin/ls -l");
	printf("system() exited with %d (status=0x%x)\n", WEXITSTATUS(ret), ret);
	return EXIT_SUCCESS;
}
```

Beispiel popen()
```c
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
int main() {
	FILE *df = popen("df -k --output=pcent . 2>/dev/null", "r");
	if (!df) PERROR_AND_EXIT("popen: df -k .");
	char line[BUFSIZ], *end = NULL;
	long int used = -1;
	while(fgets(line, BUFSIZ, df)) {
		used = strtol(line, &end, 10);
		if (end && end != line && *end == '%') break; // line is spaces-number%-newline
		used = -1;
	}
	if (pclose(df)) PERROR_AND_EXIT("pclose()");
	if (used < 0 || used > 100) {
		errno = ERANGE;
		PERROR_AND_EXIT("df -k .");
	}
	char *msg
		= used < 60 ? "Plenty of disk space (%d%% available)\n"
		: used < 80 ? "Maybe some future disk space problems (%d%% available)\n"
		: used < 90 ? "Need to clear out files (%d%% available)\n"
		: "You may face soon some severe disk space problems (%d%% available)\n";
	printf(msg, 100-used);
	return EXIT_SUCCESS;
}

```
### Thread
Threadfunktion wird angegeben, die ausgeführt werden sollte (keine Kopie). Terminiert, wenn Funktion verlassen wird.

![[Pasted image 20240612202957.png#invert]]
![[Pasted image 20240612203008.png#invert]]

Achtung, fehlendes join bzw. detach führt dazu, dass Thread-Ressourcen nie freigegeben werden.

Beispiel 1

```c
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>
#include <unistd.h>
#include <pthread.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
#define CHECKED_PTHREAD(C) do { int ret = (C); if (ret) { errno = ret; PERROR_AND_EXIT(#C); } } while(0)
void *worker(void *arg) {
	printf("worker\n");
	sleep(3);
	static int ret_value = 123;
	return &ret_value;
}

int main() {
	pthread_t thread;
	CHECKED_PTHREAD(pthread_create(&thread, NULL, worker, NULL)); // gibt im Success-Fall Thread ID zurück (0)
	printf("main\n");
	static void *retval;
	CHECKED_PTHREAD(pthread_join(thread, &retval));
	printf("worker retval = %d\n", *((int*)retval));
	exit(EXIT_SUCCESS);
}
```
 
 Beispiel 2
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

void *myturn(void *arg) {
    int *iptr = (int *)malloc(sizeof(int));
    *iptr = 5;
    for (int i = 0; i < 8; i++) {
        sleep(1);
        printf("My Turn! %d %d\n", i, *iptr);
        (*iptr)++;
    }
    // what if we return a value?
    return iptr;
}

void yourturn() {
    // Your code here
}

int main() {
    pthread_t newthread;
    int *result;

    pthread_create(&newthread, NULL, myturn, NULL);
    yourturn();

    // wait until the thread is done before we exit.
    pthread_join(newthread, (void **)&result);
    printf("thread's done: *result=%d\n", *result);
    free(result);  // Remember to free the allocated memory
    return 0;
}
```
#### Terminieren eines Threads
- return
- pthread_exit (inkl Möglichkeit für Return Wert)
- exit
- pthread_cancel (von aussen abgebrochen)
## Probleme
- vor fork() File Deskriptoren handeln (mit close)
- Child immer unmittelbar nach fork() neues Image starten mit execv() => damit laufende Threads zerstören um Synchronisierung sicherzustellen
- Für Thread-Identität thread_t() Werte benutzen statt getttid()
## Interprozess-Kommunikation
![[Pasted image 20240612203654.png#invert]]
### Signals
- Prozess kann beliebigem Prozess Signal senden
- Signal ist eine Zahl mit systemweit definierter Bedeutung
- Kernel sorgt für Benachrichtigung des angesprochenen Prozesses
- Aktionen
	- default
	- ignore
	- handler
![[Pasted image 20240612204218.png#invert]]

Weitere Befehle
- kill: sendet Signal-Code an Prozess
- pause(): Prozess blockiert bis Signal ankommt
- wifexited(), wifexitedstatus(): Fragt Exit Code von wait() ab
- wifsignaled(), wtermsig(): fragt Signal Wert des wait() ab
- sigaction(): eigene Handler-Funktion defiieren
- raise(): sendet eigenem Prozess ein Signal (Convenience-Funktion für kill)

```c
#include <sys/types.h>
#include <signal.h>
...
// tell the child to gracefully terminate, e.g. save unsaved changes and then terminate
if (kill(child_pid, SIGTERM) == -1) PERROR_AND_EXIT("kill(SIGTERM)");
...
```

Beispiel
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
static pid_t start_child(int wait_for_signal) {
	pid_t cpid = fork();
	if (cpid == -1) PERROR_AND_EXIT("fork");
	if (cpid > 0) return cpid; // the parent returns the child pid
	if (wait_for_signal && pause() == -1) PERROR_AND_EXIT("pause"); // one child waits for a signal
	exit(123); // the child exits normally
}
static void wait_for_child() {
	int wsts;
	pid_t wpid = wait(&wsts); // wait blocking for any child to terminate
	if (wpid == -1) PERROR_AND_EXIT("wait");
	if (WIFEXITED(wsts)) printf("Child %d: exit=%d (status=0x%04X)\n", wpid, WEXITSTATUS(wsts), wsts);
	if (WIFSIGNALED(wsts)) printf("Child %d: signal=%d (status=0x%04X)\n", wpid, WTERMSIG(wsts), wsts);
}

int main() {
	pid_t cpid1 = start_child(0); // start child that exits with exit code
	pid_t cpid2 = start_child(1); // start child that waits for signal to terminate
	printf("Children started: %d (term with exit), %d (term with signal)\n", cpid1, cpid2);
	sleep(1); // let the children start so that both child processes exist
	if (kill(cpid2, SIGTERM) == -1) PERROR_AND_EXIT("kill"); // tell the child to terminate gracefully
	wait_for_child(); // waits blocking until some child terminates
	wait_for_child(); // waits blocking until some child terminates
}
```

Beispiel setaction(): Aufsetzen von Signal
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
#include <signal.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
static void handler(int sig, siginfo_t *siginfo, void *context) {
	printf("caught(%d): source=%d, this=%d\n", sig, siginfo->si_pid, getpid());
	raise(SIGTERM); // send SIGTERM to itself (identical to kill(getpid(), SIGTERM))
}
static void set_handler(int sig, void (*handler)(int, siginfo_t *, void *)) { 
	struct sigaction a = { 0 };
	a.sa_flags = SA_SIGINFO; // handler variant with additional signal info signature
	a.sa_sigaction = handler; // the handler to be registered, alternative SIG_IGN for ignore
	if (sigfillset(&a.sa_mask) == -1) PERROR_AND_EXIT("sigfillset"); // block all Signals
	if (sigaction(sig, &a, NULL) == -1) PERROR_AND_EXIT("sigaction"); // register handler
}
static pid_t start_child() {
	pid_t cpid = fork();
	if (cpid == -1) PERROR_AND_EXIT("fork");
	if (cpid > 0) return cpid; // parent returns cpid
	set_handler(SIGUSR1, handler); // child...
	if (pause() == -1) PERROR_AND_EXIT("pause");
	exit(EXIT_FAILURE);
}

int main() {
	pid_t cpid = start_child(); // start child that waits for signal to terminate
	printf("parent=%d, child=%d\n", getpid(), cpid);
	sleep(1); // give time to the child to start
	if (kill(cpid, SIGUSR1) == -1) PERROR_AND_EXIT("kill"); // send signal to child
	int ws;
	if (wait(&ws) == -1) PERROR_AND_EXIT("wait");
	if (WIFEXITED(ws)) printf("child exit=%d (status=0x%04X)\n", WEXITSTATUS(ws), ws);
	if (WIFSIGNALED(ws)) printf("child signal=%d (status=0x%04X)\n", WTERMSIG(ws), ws);
}

```
#### Zu beachten
- Signal Settings bei fork() mitvererbt
- Signal handling in Multi-Threaded Prozessen schwierig
### POSIX Pipe

![[Pasted image 20240612205153.png#invert]]

- FIFO Byte-Buffer von fixer Maximalgrösse
- jedes Ende des FIFO wird mit einem eigenen File Deskriptor angesprochen
- unidirektional, d.h. es wird an einem Ende geschrieben, am anderen gelesen
- lesen und schreiben ist implizit synchronisiert
#### Anonymous Pipe
mit `pipe(int [2]` gefolgt von fork():
- zwei Filedeskriptoren, auf dem einen wird geschrieben und auf dem anderen gelesen
- Datenaustausch synchron oder asynchron
- unidirektional, für bidirektional zwei Pipes erstellen
- kann mit `close()` wieder geschlossen werden
- `read()` zum Lesen
- `write()` zum Schreiben

Beispiel 1
```c
#include <sys/types.h>
#include <unistd.h>
//...
int fd[2];
pipe(fd);
pid_t cpid = fork();
// ...
if (cpid > 0) { // still in parent process: read from pipe
	close(fd[1]); // close write-file-descriptor
	read(fd[0], ...); // use read-file-descriptor
//...
} else { // in child process: write to pipe
	close(fd[0]); // close read-file-descriptor
	write(fd[1], ...); // use write-file-descriptor
}
```

Beispiel 2
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
#define PERROR_AND_EXIT(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
#define MESSAGE "blocking pipe example message...\n"
#define MSIZE 10
int main()
{
	int fd[2];
	if (pipe(fd) == -1) PERROR_AND_EXIT("pipe");
	pid_t cpid = fork();
	if (cpid == -1) PERROR_AND_EXIT("fork");
	if (cpid > 0) { // still in parent process: read from pipe
		if (close(fd[1]) == -1) PERROR_AND_EXIT("close");
		int n;
		do {
			char msg[MSIZE];
			n = read(fd[0], msg, MSIZE);
			if (n == -1) PERROR_AND_EXIT("read");
			write(STDOUT_FILENO, msg, n);
		} while (n > 0);
		if (close(fd[0]) == -1) PERROR_AND_EXIT("close");
		if (wait(NULL) == -1) PERROR_AND_EXIT("wait");
	} else { // in child process: write to pipe
		if (close(fd[0]) == -1) PERROR_AND_EXIT("close");
		if (write(fd[1], MESSAGE, sizeof(MESSAGE)) == -1) PERROR_AND_EXIT("write");
	}
}
```
#### Named Pipe
Kreiert ein File, das mittels I/O normal geschrieben/gelesen werden kann.

```c
#include <sys/types.h>
#include <sys/stat.h>

int mkfifo(const char *pathname, mode_t mode);
```

Zugriff wie bei regulärem File.
### Message Queue
- strukturiert
- bidirektional
- mehrere Leser und Schreiber

Befehle
- `mq_open()` Kreiert Message Queue mit gegebener Dimension und Zugriffsrechten und existiert auf virtuellem Filesystem /dev/mqueue
- `mq_close()` gibt Kernel bekannt, dass Zugriffe geschlossen sind
- `mq_unlink()` löscht Queue von Filesystem
- `mq_receive()`
- `mq_send()` inkl. Prio
- `mq_getattr()`Gibt unter anderem Anzahl Messages der Queue zurück
- `mq_notify()`Gibt aus, wie Prozess benachrichtigt werden soll

Beispiel 1
```c
#include <sys/types.h>
#include <unistd.h>
#define MSIZE 100
//...
	char msg[MSIZE];
	struct mq_attr a = { .mq_maxmsg = 10, .mq_msgsize = MSIZE };
	q = mq_open("/my-queue", O_CREAT|O_RDWR, 0666, &a); // queue name must start on a /
	pid_t cpid = fork();
	//...
	if (cpid > 0) { // still in parent process: read from queue
		//...
		mq_receive(q, msg, MSIZE, NULL);
		//...
		mq_close(q)
	} else { // in child process: write to queue
		mq_send(q, msg, MSIZE, prio);
//..
```
### POSIX Socket
- virtueller Stecker gegeben durch IP-Adresse der Netzwerkkarte plus Port-Nummer
- zwei Maschinen können über diese virtuellen Stecker eine Verbindung aufbauen über welche ein Protokoll der Wahl transportiert wird (bspw. UDP, TCP)
- Auf ein und derselben Maschine auch als IPC anwendbar
- verbindungsorientiert (Client/Server)
- Zugriff über File-Deskriptoren

![[Pasted image 20240612210557.png#invert]]
### Alternativen

- Shared Memory
- Shared File
## Inter-Thread Kommunikation

### Probleme
- Race Condition: System abhängig von Reihenfolge der Tasks
- Synchronisation: Vermeidung von Race Conditions
### Synchronisationsarten
- Sperren (Stop & Go)
- Signalisieren
- Warten
- Zeitlich exklusiver Zugriff
- Critical Section
- Gegenseitiger Ausschluss
	- Mutex (ein Task schliesst ein anderer aus)
### Critical Section - Mutex

- Gemeinsame Daten und Ressourcen schützen
- Konzept: Schloss
- Init, Lock und Unlock
- Performance-Einbussen
- Lock-Unlock Paare über verschiedene Tasks - technisch möglich aber nicht vorgesehen
- Deadlock möglich
- kann mit Semaphore nachgebaut werden

![[Pasted image 20240612210944.png#invert]]

**Critical Section Problem Beispiel**
Die Statements, welche die geteilte Ressource (value) modifizieren, dürfen nicht durch einen Task-Kontextswitch unterbrochen werden.

```c
#include <sys/types.h>
#include <pthread.h>
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
#define FATAL(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
// for the demo: increases the chance that a context switch happens at an undesired place
#define N 100000000

volatile int value = 0; // shared variable: read and written in both threads

void * count(void *arg)
{
	int delta = *(int*)arg; // increment or decrement (arg is +1 or -1)
	for(int i = 0; i < N; i++) {
		// Problem: task context switch may happen everywhere, i.e. also here
		int a = value; // read shared variable
		// Problem: task context switch may happen everywhere, i.e. also here
		a += delta; // modify
		// Problem: task context switch may happen everywhere, i.e. also here
		value = a; // write shared variable
		// Problem: task context switch may happen everywhere, i.e. also here
	}
	return NULL;
}

int main(void)
{
	pthread_t th_inc;
	pthread_t th_dec;
	int inc = +1;
	int dec = -1;
	if (pthread_create(&th_inc, NULL, count, &inc) != 0) FATAL("create");
	if (pthread_create(&th_dec, NULL, count, &dec) != 0) FATAL("create");
	if (pthread_join(th_inc, NULL) != 0) FATAL("join");
	if (pthread_join(th_dec, NULL) != 0) FATAL("join");
	// N times increment and N times decrement is expected to result in value 0 again
	if (value != 0) fprintf(stderr, "ERROR: exp=%d, act=%d\n", 0, value);
}
```

**Lösung Beispiel**
```c
#include <sys/types.h>
#include <pthread.h>
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
#define FATAL(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
// for the demo: increases the chance that a context switch happens at an undesired place

#define N 100000000
volatile int value = 0; // shared variable: read and written in both threads
pthread_mutex_t mutex;

void * count(void *arg)
{
	int delta = *(int*)arg; // increment or decrement (arg is +1 or -1)
	for(int i = 0; i < N; i++) {
		if (pthread_mutex_lock(&mutex) != 0) FATAL("lock");
		int a = value; // read shared variable
		a += delta; // modify
		value = a; // write shared variable
		if (pthread_mutex_unlock(&mutex) != 0) FATAL("unlock");
	}
	return NULL;
}

int main(void)
{
	if (pthread_mutex_init(&mutex, NULL) != 0) FATAL("mutex_init");
	pthread_t th_inc;
	pthread_t th_dec;
	int inc = +1;
	int dec = -1;
	if (pthread_create(&th_inc, NULL, count, &inc) != 0) FATAL("create");
	if (pthread_create(&th_dec, NULL, count, &dec) != 0) FATAL("create");
	if (pthread_join(th_inc, NULL) != 0) FATAL("join");
	if (pthread_join(th_dec, NULL) != 0) FATAL("join");
	// N times increment and N tmies decrement is expected to result in value 0 again
	if (value != 0) fprintf(stderr, "ERROR: exp=%d, act=%d\n", 0, value);
}

```

#### Rekursive Locks
Ein Mutex muss wissen, in welchem Task der Lock passierte und entsprechendes Fehlerhandling machen. Dieses Wissen über die aktuell blockierende Task kann genutzt werden, um verschachtelte (rekursive) Lock-Unlock Paare sinnvoll zu meistern.

Beispiel
```c
Mutex = { allow_recursion }; // Pseudo code
Container shared_container = { ... };
void get_length(Container c)
{
	lock(mutex);
	int len = count(c.data);
	unlock(mutex);
	return len;
}

void append(Container c, Element e)
{
	lock(mutex);
	// get_length() locks and unlocks again in the same thread as the outer lock-unlock pair
	if (get_length(c) < c.capacity) {
		push_back(c.data, e);
	}
	unlock(mutex);
}
```

![[Pasted image 20240612211834.png#invert]]
### Warten / Signalisieren - Semaphore

- Konzept: Ampel
- Zähler, wie viele Tasks durchgelassen werden sollen (wenn Zähler auf 0, Task blockiert)
- Gebraucht wenn bspw. ein Prozess Daten generiert und ein anderer konsumiert
- kostet Zeit
- Risiko für fehlende Signale
- Rekursion nicht möglich
- Deadlock

![[Pasted image 20240612211128.png#invert]]

**Warten Problem Beispiel**
An notwendigen Synchronisationspunkten muss mit geeigneten Mitteln aufeinander gewartet werden

```c
#include <sys/types.h>
#include <pthread.h>
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
#include <limits.h>
#define FATAL(M) do { perror(M); exit(EXIT_FAILURE); } while(0)
#define CHECK(E,A,M) if((E)==(A));else fprintf(stderr,"ERROR: "M": exp=%d, act=%d\n",E,A)
#define N 10000

volatile int array[N] = { 0 }; // shared variable: init in one thread, then use in both

void *min(void *arg) // initialize the data and calculate min value of all
{
	for(int i = 0; i < N; i++) array[i] = i - N/2; // init the shared data -N/2...N-1-N/2
	// missing sync: notify (signal) here that the initialization is completed
	int value = INT_MAX;
	for(int i = 0; i < N; i++) if (value > array[i]) value = array[i];
	CHECK(-N/2, value, "wrong min value");
	return NULL;
}

void *max(void *arg) // calculate max value of already initialized data
{
	// missing sync: wait here until the initialization is completed
	int value = INT_MIN;
	for(int i = 0; i < N; i++) if (value < array[i]) value = array[i];
	CHECK(N-1-N/2, value, "wrong max value");
	return NULL;
}

int main(void)
{
	// missing sync: mark here that the initialization is not completed yet
	pthread_t th_max;
	pthread_t th_min;
	if (pthread_create(&th_max, NULL, max, NULL) != 0) FATAL("create");
	if (pthread_create(&th_min, NULL, min, NULL) != 0) FATAL("create");
	if (pthread_join(th_max, NULL) != 0) FATAL("join");
	if (pthread_join(th_min, NULL) != 0) FATAL("join");
}
```

**Lösung Beispiel**
![[Pasted image 20240612211957.png#invert]]
### Weitere Mittel
- Monitor
	- Ressource-Objekt mit eingebauter Synchronisation
	- für interne Zugriffe: Mutex
	- wird in Java verwendet
- Barrier
	- blockiert mehrere Tasks (Gegenstück zu Semaphore)
- Container
	- MQ
### Probleme
- Deadlock
- Livelock
	- das System ist nicht im Sinne eines Deadlock blockiert, sondern die Tasks sind so beschäftigt «sich aus dem Weg zu gehen», dass sie keine produktive Arbeit mehr leisten → Zugriffskonflikte anders lösen
- Starvation
	- eine blockierte Task kommt nie an die Reihe, weil andere Tasks sich «vordrängen», z.B. beim Unlock einer Mutex → das OS sollte dafür sorgen, dass dies nicht passiert
- Priority Inversion
	- eine Task mit tiefer Priorität blockiert eine Task mit höherer Priorität → das OS sollte dies erkennen und z.B. der blockierenden Task bis zur Lösung der Blockade die höchste Priorität der blockierten Tasks geben (Priority Inheritance)
### Beispiele
![[Pasted image 20240612212614.png#invert]]
