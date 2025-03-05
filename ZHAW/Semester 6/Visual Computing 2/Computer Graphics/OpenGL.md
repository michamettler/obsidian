#sem6 #visualcomputing/computer-graphics 

## Programmable Shaders
### Vertex Shader
Purpose: (Optional stage) Takes entire primitives (points, lines, triangles) as input and can generate new primitives on the fly.
Key Tasks:
- Add or remove vertices, creating new geometry (e.g., silhouette outlines, particle generation).
- Access adjacency data if available, enabling operations that depend on neighbouring primitives.
- Output modified or newly created primitives to the rasterizer.
A “custom workshop” stage—allows you to reshape or expand the geometry before rasterization.
![[OpenGL-1740402626500.webp#invert]]
### Fragment Shader
Purpose: Operates on fragments (potential pixels) after rasterization, determining final color and depth.
Key Tasks:
- Apply lighting, texturing, and other per-pixel effects (bump maps, shadows).
- Implement advanced shading algorithms (e.g., Phong shading).
- Output color, depth, or other data (like normals for postprocessing).
The “finishing touch” stage—where each pixel’s final look is decided before it’s drawn.
![[OpenGL-1740402776059.webp#invert]]
## OpenGL Primitives
![[OpenGL-1740402847086.webp#invert]]

### Konvex
![[OpenGL-1740402906005.webp#invert]]

Linie möglich zwischen 1 und 4, damit kommt OpenGL nicht klar (nicht konvex).
![[OpenGL-1740403080836.webp#invert]]
### Tessellation
![[OpenGL-1740402994506.webp#invert]]
=> tessellation = alle Elemente zu Dreiecken machen
## Efficiency
Reduce the number of function calls
- Pass arrays of vertices instead of single ones
Store data on GPU and do not resend data
- Display List
## PyOpenGL Code Examples
### Setup Window
```python
from OpenGL.GL import *
from OpenGL.GLUT import *
from OpenGL.GLU import *

screen_width = 1000
screen_height = 800
background_color = (0.0, 0.0, 0.0, 1.0)

def main():
	"""
	Main function to set up the window and start the GLUT main loop.
	"""
	# Initialize GLUT with command-line parameters.
	glutInit(sys.argv)
	
	# Set up display mode:
	# - GLUT_RGBA: use RGBA color mode.
	# - GLUT_DOUBLE: enable double buffering.
	# - GLUT_ALPHA: use an alpha channel.
	# - GLUT_DEPTH: enable depth buffering. !! important for 3D
	glutInitDisplayMode(GLUT_RGBA|GLUT_DOUBLE|GLUT_ALPHA |GLUT_DEPTH) 
	
	# Set up window size
	glutInitWindowSize(screen_width, screen_height)
	
	# Set up window position.
	glutInitWindowPosition(0, 0)
	
	## SETUP WINDOW
	glutCreateWindow(b"PyOpenGL Window Setup")
	
	# initialize the context
	R,G,B,A = background_color
	glClearColor(R,G,B,A)
	
	# Register the display callback function.
	glutDisplayFunc(display)
	
	# Register the keyboard callback to handle key presses.
	glutKeyboardFunc(keyboard)
	
	# Optionally, register the idle callback to continuously
	update the window.
	glutIdleFunc(display)
	
	# Enter the GLUT main loop.
	glutMainLoop()

def display():
	"""
	Display callback function that clears the screen and swaps
	the buffers
	"""
	# Clear color and depth buffers
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
	glLoadIdentity()
	# Any Drawing code would go here
	glutSwapBuffers() ## Double Buffer

def keyboard(key, x, y):
	"""
	Keyboard callback function.
	Exits the program when 'q' or the Escape key is pressed.
	"""
	key = key.decode("utf-8") if isinstance(key, bytes) else key
	
	if key in ['q', 'Q', '\x1b']:
		print("Quit key pressed. Exiting program.")
	try:
		# Try to exit gracefully by leaving the GLUT main loop.
		glutLeaveMainLoop()
	except Exception:
		# If glutLeaveMainLoop() is not available, force exit immediately.
		os._exit(0)
```
#### Anmerkungen:

**GLUT_DEPTH** wichtig für 3D
**glutKeyboardFunc(keyboard)** Wichtig für Tastatursteuerung (bspw. Fenster schliessen mit q)
### Rotierendes Rect

```python
spin = 0.0

def display_rect():
	global spin
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT )
	glLoadIdentity()
	glPushMatrix()
	glRotatef(spin, 0.0, 0.0, 1.0 )
	glColor4f(0.0, 1.0, 1.0, 0.5 )
	glRectf( -3.0, -3.0, 3.0, 3.0 )
	glPopMatrix()
	glutSwapBuffers()

def update_vars():
	global spin
	spin = spin + 1.0
	if spin > 360.0 :
		spin = spin - 360.0
		glutPostRedisplay()
```

### Polygons
![[OpenGL-1740404232290.webp]]

- Z-Buffer muss explizit angegeben werden, ansonsten bestimmt Reihenfolge des Zeichnens
	- `glEnable(GL_DEPTH_TEST)`
	- `glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)`
	- `glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH)`
	- `glutSwapBuffers()`
