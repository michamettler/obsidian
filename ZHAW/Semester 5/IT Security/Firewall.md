#itsecurity #sem5

![[Pasted image 20241101181907.png#invert]]
## Netfilter
Kernel has a number of hooks that are called at different points during packet processing
- Nftables rules have a classification part and one or more action parts
- Classification part says to what packets this rule applies • Action says what to do with the packet. There are several actions:
	- **accept**: continue to process the packet
	- **drop**: stop processing the packet
	- **reject**: stop processing the packet and tell the sender
	- **jump**: continue processing elsewhere (see below)
- Predominant recommendation is to drop unwanted packets
![[Pasted image 20241101182003.png#invert]]
## Firewalls Rules definieren
Rules sind in Ketten (chains) organisiert, die jeweils mit einem bestimmten Hook assoziiert sind. Innerhalb einer Chain werden die Regeln von der ersten bis zur letzten Regel abgearbeitet, solange bis eine gefunden wird, auf welche die Classification zutrifft. In diesem Fall wird die Aktion der Regel ausgewertet. Die Bearbeitung der Chain wird dann abgebrochen.
Chains haben ausserdem noch einen Typ (type). Wir nehmen hier zunächst den Typ filter, der dazu dient, Pakete zu filtern. Zuletzt besitzt jede Chain noch eine Priorität (priority). Werden Pakete akzeptiert (accept) und existiert für denselben Hook eine weitere Chain mit einer späteren (höheren) Priorität, wird das Paket durch diese später priorisierte Chain geschickt, also erneut ausgewertet. Pakete werden also solange ausgewertet, wie sie akzeptiert werden und es später priorisierte Chains gibt.
### Komponenten
- Ruleset: Enthält alle Tables
- Tables: Enthalten Chains und sind für eine bestimmte Address Family zuständig
- Chains: Enthalten Rules, sind einem bestimmten Hook zugeordnet und haben eine Priorität und eine Policy.
- Rules: Enthalten eine Klassifikation und eine Aktion. Die Klassifikation sagt, auf welche Pakete die Regel zutrifft und die Aktion sagt, was mit dem Paket innerhalb dieser Chain geschehen soll.
### Statefull Firewall
```firewall
table inet myfilter {
	chain myforward {
		type filter hook input priority 0; policy drop;
		ct state established, related accept
		ip daddr $daddr tcp dport 1234 ct sate new accept
	}
}
```

In der 4. Zeile werden alle Pakete, welche zu einer anderen Verbindung gehören (z.B. Acknowledgements in einer TCP Verbindung, Echo-Reply Packete, welche zu einem Echo Request gehören, etc.) zugelassen. In der 5. Zeile wird mit ct sate new accept angegeben, dass das jetzt eine neue Verbindung ist, für welche auch der Rückweg zugelassen werden soll.
### Beispiel Praktikum
![[Pasted image 20241101182653.png#invert]]
Geht immer über Firewall, sprich dort werden die Rules definiert:

```firewall
define difc = ens4                     # Interface name to DMZ network
define d4nw = 10.0.2.0/24      # DMZ IPv4 network
define d4ad = 10.0.2.5# DMZ IPv4 address

define eifc = ens5# Interface name to external network
define e4nw = 10.0.3.0/24      # External IPv4 network
define e4ad = 10.0.3.5# External IPv4 address

flush ruleset

table inet myfilter {
  chain myinput {
		type filter hook input priority 0; policy drop;
		# DO NOT CHANGE OR COMMENT THE FOLLOWING LINE
		ip saddr 10.0.1.254 tcp dport 22 accept;
		
		# INT Ping to firewall
		iifname $iifc ip saddr $i4nw icmp type echo-request accept;
		
		# DMZ Ping to firewall ping
		iifname $difc ip saddr $d4nw icmp type echo-request accept;
  }
  
  chain myoutput {
		type filter hook output priority 0; policy drop;
		
		# DO NOT CHANGE OR COMMENT THE FOLLOWING LINE
		ip daddr 10.0.1.254 tcp sport 22 accept;
		
		# Ping reply to INT
		iifname $iifc ip daddr $i4nw icmp type echo-reply accept;
		
		# Ping reply to INT
		iifname $difc ip daddr $d4nw icmp type echo-reply accept;
		
		#ct state established,related accept;
  }
  
  chain myforward {
		type filter hook forward priority 0; policy drop;
	
		# INT to DMZ: Allow SSH
		iifname $iifc ip saddr $i4nw oifname $difc ip daddr $d4nw tcp dport ssh ct state new accept;
		#iifname $difc ip saddr $d4nw oifname $iifc ip daddr $i4nw tcp sport ssh accept;
		
		# INT to DMZ: Allow Ping
		        iifname $iifc ip saddr $i4nw oifname $difc ip daddr $d4nw icmp type echo-request ct state new accept;
		        #iifname $difc ip saddr $d4nw oifname $iifc ip daddr $i4nw icmp type echo-reply accept;
		
		# INT to EXT: Allow Ping
		iifname $iifc ip saddr $i4nw oifname $eifc ip daddr $e4nw icmp type echo-request ct state new accept;
		#iifname $eifc ip saddr $e4nw oifname $iifc ip daddr $i4nw icmp type echo-reply accept;
		
		# INT to EXT: Allow any TCP
		iifname $iifc ip saddr $i4nw oifname $eifc ip daddr $e4nw tcp dport != 0 ct state new accept;
		
		# EXT to DMZ: Allow SSH & FTP
		iifname $eifc ip saddr $e4nw oifname $difc ip daddr $d4nw tcp dport {ssh, 20, 21 } ct state new accept;
		#iifname $difc ip saddr $d4nw oifname $eifc ip daddr $e4nw tcp sport {ssh, 20, 21 } accept;
		
		# DMZ to EXT: Allow Ping
		iifname $difc ip saddr $d4nw oifname $eifc ip daddr $e4nw icmp type echo-request ct state new accept;
		#iifname $eifc ip saddr $e4nw oifname $difc ip daddr $d4nw icmp type echo-reply accept;
		        
		#allow traceroute
		iifname $iifc ip saddr $i4nw oifname $eifc ip daddr $e4nw udp dport {33434-33523} ct state new accept;
		
		# Make stateful: Allow related and established connections
		ct state established,related accept;
	}
}
```