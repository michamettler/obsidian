#visualcomputing/computer-graphics #sem5 
## Shading
- Light-material interactions cause each point to have a different color or shade
- Light that strikes an object is partially absorbed and partially scattered (reflected)
- The amount reflected determines the color and brightness of the object
	- A surface appears red under white light because the red component of the light is reflected and the rest is absorbed
- The reflected light is scattered in a manner that depends on the smoothness and orientation of the surface
## Scattering
- Scattering
	- Light strikes A
		- Some scattered
		- Some absorbed
	- Some of scattered light strikes B
- The smoother a surface, the more reflected light is concentrated in the direction a perfect mirror would reflect the light
- A very rough surface scatters light in all directions
## Shininess
- Distribution of scattered light is not equally in all directions and depends on material
- Normalized (gaussian) distribution
![[Pasted image 20250109175955.png#invert]]
## Shading
- More light is scattered along ideal reflection vector
- Normal is determined by local orientation of surface
- Angle of incidence == angle of reflection
- Surfaces oriented as ideal reflector between light source and observer are seen brighter
## Light Reflection
![[Pasted image 20250109180516.png#invert]]