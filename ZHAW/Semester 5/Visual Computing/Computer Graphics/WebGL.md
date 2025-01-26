#visualcomputing/computer-graphics #javascript #sem5 
## Three.js
### Richtungen
```js
context.beginPath();
context.moveTo(100, 100); // Startpunkt
context.lineTo(150, -150); // Linie nach rechts und nach oben
context.stroke();
```

### Example

```html
<body>
	<div id="webgl-container"></div>
	<script type="text/javascript" src="js/three.js"></script>
	<script type="text/javascript">
		var scene = new THREE.Scene();
		var camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 800);
		var renderer = new THREE.WebGLRenderer();
		renderer.setClearColor(0xEEEEEE, 1.0);
		renderer.setSize(window.innerWidth, window.innerHeight);
		renderer.setPixelRatio(window.devicePixelRatio);
		var webglContainer = document.getElementById('webgl-container');
		webglContainer.appendChild(renderer.domElement);
		var axes = new THREE.AxisHelper(20);
		scene.add(axes);
		 // position and point the camera to the center of the scene
		camera.position.x = -8;
		camera.position.y = 10;
		camera.position.z = 20;
		camera.lookAt(scene.position);
		renderer.render(scene, camera);
	</script>
</body>
```
### Scene Graph
![[Pasted image 20241117170049.png#invert]]
![[Pasted image 20241117170151.png#invert]]
#### Object3D
- Node "Instance"
- Transformation matrix
- Children array

#### Mesh
- Subclass of Object3D
- [[#Mesh Geometry]] (shared)
- Material (shared)
	- Defines the way color is calculated on geometry surfaces
##### Illustration of shared Geometry and Material
![[Pasted image 20241117170330.png#invert]]
### Operations
#### Mesh Geometry

```js
var geometry = new THREE.Geometry();
geometry.vertices.push(
 new THREE.Vector3( -10, 10, 0 ),
 new THREE.Vector3( -10, -10, 0 ), new THREE.Vector3( 10, -10, 0 )
);
geometry.faces.push( new THREE.Face3( 0, 1, 2 ) );
```
#### Extrude
![[Pasted image 20241117165828.png]]
```js
var arrow = new THREE.Shape([ new THREE.Vector2(0, 3),
 new THREE.Vector2(3, 3), new THREE.Vector2(3, 4), new THREE.Vector2(5, 2), new THREE.Vector2(3, 0), new THREE.Vector2(3, 1),
 new THREE.Vector2(0, 1), new THREE.Vector2(0, 3) ]);
var geom = new THREE.ExtrudeGeometry(arrow, {
 bevelEnabled: false, amount: 1.5 });
```