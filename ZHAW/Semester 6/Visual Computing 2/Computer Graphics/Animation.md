#sem6 #visualcomputing/computer-graphics 

https://www.youtube.com/watch?v=8gi9lUYMRcI&t=1s
## Flickering
- When displays refresh is below 60 Hz then the visual system sees flickering on the display
	- The perception of flickering is higher when contrast is higher 
	- This flickering can also be seen at higher display rates when objects move (fast) on the screen
- Two options for animating in WebGL/three.js
	- Interval timer → every 16 ms
	- requestAnimFrame → connected to display refresh rate
## Double Buffering
- Animation with real time graphics uses double buffering to present sequence of rendered images
	- Always render into a buffer that is not displayed
	- When rendering of scene is done, swap buffer
- Prevents display of a partial rendering
- Double buffering
	- Always display front buffer
	- Rendering into back buffer
	- Trigger a buffer swap (switch pointer of back & front buffer)
	- Render next frame into back buffer
	- Swap buffer
## Motion vs. Deformation
![[Animation-1741007720828.webp#invert]]
## Animation in Film
![[Animation-1741007993427.webp#invert]]
### Workflow
![[Animation-1741008025630.webp#invert]]
## Anim Principles
1. Squash and stretch
	1. Form der Objekte verformen bei Animation (Ball springt)
2. Timing 
	1. Animationen nicht zu schnell und nicht zu langsam
3. Anticipation
	1. Animation ankündigen (in die Hocke gehen vor Sprung)
4. Staging 
	1. wichtiges in Vordergrund
5. Follow through and overlapping action
	1. Actions dauern länger als der Hauptpart (Ballwerfen, Arm bewegt sich weiter)
6. Straight ahead action and pose-to-pose action
7. Slow in and slow out
	1. Acceleration bei Auto
8. Arcs
	1. Natürliches Movement
9. Exaggeration
	1. Alles übertreiben für Engagement
10. Secondary action
	1. Eigenleben für sekundäre Objekte (Kabel bei Pixar)
11. Appeal
	1. Verschiedene Shapes für verschiedene Charaktere
## Speed Control (ease-in ease-out)
![[Animation-1741008802555.webp#invert]]
**Wichtig, Position kontinuierlich (Ease-Out)**
### Curve Fitting
![[Animation-1741008877743.webp#invert]]
## Skeleton Animations
![[Animation-1741010235121.webp#invert]]
## Kinematics
- Forward kinematics (FK): Define the movements at each joint
	- the rotation parameters of all joints are manipulated and the corresponding transforms are actualized
	- A complete set of rotations on the whole angles is called a pose (a vector of rotations)
	- Forward kinematics is not user-friendly
	- ![[Animation-1741013731658.webp#invert]]
- Inverse kinematics (IK): Define the movements at the end points and compute the angles required at each joint
	- Instead of specifying the whole links, the animator might want to specify the end position of the effector
	- The computer calculates then the angles of the other joints
	- Unfortunately analytical solutions only work for simple cases
	- usually pre-written scripts
	- ![[Animation-1741013803602.webp#invert]]
## Warping
![[Animation-1741010323019.webp#invert]]
## Blendshapes
![[Animation-1741013871633.webp]]
## Physics Simulation
- Model physical behaviour to calculate animations automatically (no manual editing of keyframes)
- Rigid Body Dynamics / Rigid Body Simulation
- [[Bezugssysteme in Unity]]
## Collisions
![[Animation-1741014994401.webp#invert]]
### Particle Systems
- e.g. fire, smoke, explosions, etc.
![[Animation-1741015076340.webp#invert]]
## Motion Capturing
- An alternative to the synthetic generation of movement is the recording of the movement of real humans
- This is called motion capture
	- Real humans are equipped with sensors (or markers) applied to the different body parts
	- The xyz positions of these markers in time are recorded while the „actor“ is performing movement