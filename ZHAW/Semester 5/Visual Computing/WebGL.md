#visualcomputing #javascript #sem5 
## Three.js

Example
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

