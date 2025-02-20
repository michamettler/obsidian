#visualcomputing/computer-graphics #sem6

Schauen: https://www.youtube.com/watch?v=DuQDx0ZIxa8
## Textures
- Texturing can be thought of as pasting an image onto a surface
![[Pasted image 20250220213627.png]]
![[Pasted image 20250220213636.png#invert]]
- Rendering a texture is similar to Gourad shading (Interpolation)
- **Linear Interpolation cannot be used!**
### Aliasing
![[Pasted image 20250220213718.png#invert]]
#### Example
![[Pasted image 20250220214603.png#invert]]

### Modulate
Increase the texture quality by modulation.
![[Pasted image 20250220213835.png]]
## Texture Filtering
- Usually the size of a texel isn't equal to the size of the corresponding pixel.
- The rule, which texel is mapped, is called a filter
![[Pasted image 20250220214420.png#invert]]

### MIP Maps
[[#Aliasing]] can occur (artifacts/aliasing at details).
![[Pasted image 20250220214116.png#invert]]
![[Pasted image 20250220214136.png]]
## Normal Mapping
- To give a surface a rough appearance without modelling it in detail.
- Idea: Use a texture (this time not an image) to modulate the surface normal in a controlled fashion
![[Pasted image 20250220214627.png]]
### Normal Mapping vs. Bump Mapping
![[Pasted image 20250220214803.png]]
#### Normal
- A normal map defines the normal for each fragment
- A normal map is a texture, where the normals are coded as color components (red, green and blue).
- Since the z-component of the normal map maps to the blue color component, bump maps in general look blueish.
![[Pasted image 20250220214707.png#invert]]
#### Bump
![[Pasted image 20250220214729.png#invert]]
## Environment Mapping
- Environment mapping is a shortcut to render shiny objects that reflect the environment in which they are placed.
- An environment map is a texture.
- It is mapped to the object like a texture.
![[Pasted image 20250220214907.png]]
- Compute the reflected ray of the view vector using the normal at the point of intersection.
- Decide which face of the cube is hit by this ray.
- Compute coordinates in environment map.
- Set vertex color according to map.
### Cube Maps vs. Sphere Maps
Sphere Map is simpler, however cubic is more commonly used.
![[Pasted image 20250220214930.png#invert]]
![[Pasted image 20250220215005.png#invert]]
## Shadow Maps
![[Pasted image 20250220215120.png#invert]]
## Illumination Models
![[Pasted image 20250220215659.png#invert]]
## Raytracing

**REPETIEREN**
![[Pasted image 20250220215538.png#invert]]
![[Pasted image 20250220215247.png]]