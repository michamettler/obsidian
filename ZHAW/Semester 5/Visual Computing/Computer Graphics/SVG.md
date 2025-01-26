#visualcomputing/computer-graphics  #sem5 
### HTML Canvas
- Create canvas within HTML DOM
- Draw on canvas via JavaScript
- Use '2D’ context for drawing
- Ursprung 0,0 ist oben links

```html
<body>
	<H1>HTML5 Canvas: My first line</H1>
	here we go ... <br>
	<canvas id="myCanvas" width="400" height="200"></canvas>
	<script>
		var canvas = document.getElementById('myCanvas');
		var context = canvas.getContext('2d');
		context.beginPath();
		context.moveTo(100, 150);
		context.lineTo(350, 50);
		context.lineWidth = 10;
		context.strokeStyle = '#0000ff';
		context.stroke();
	</script>
	<br>Example of CGR Computer Graphics course at ZHAW.
</body>
```
![[Pasted image 20240930161117.png]]
### SVG-Elements

Descriptive XML file format
<svg xmlns="http://www.w3.org/2000/svg">
	<circle cx="75" cy="75" r="50" fill="blue" />
</svg>

Elements
```html
// Basic Shapes
<svg xmlns=http://www.w3.org/2000/svg xmlns:xlink="http://www.w3.org/1999/xlink" >

	<rect x="25" y="25" width="100" height="75" fill="green" stroke="black" stroke-width="5"/>
	<rect x="150" y="25" rx="20" ry="20" width="100" height="75“ fill="green" stroke="black"/>
	<circle cx="350" cy="75" r="50" fill="orange" stroke="black" stroke-width="5"/>
																				 
	<ellipse cx="525" cy="75" rx="100" ry="50" fill="yellow" stroke="black" stroke-width="5"/>
	
	<line x1="25" y1="190" x2="150" y2="150" stroke="black" stroke-width="1"/>
	<line x1="25" y1="200" x2="150" y2="180" stroke="black" stroke-width="4"/>
	<line x1="25" y1="220" x2="150" y2="220" stroke="black" stroke-width="8"/>
	<line x1="25" y1="240" x2="150" y2="290" stroke="black" stroke-width="16"/>
	
	<polyline points="230,260 250,200 280,300 320,160 420,160 420,200" fill="none" stroke="black“/>
	<polygon points="450,260 540,180 660,300" fill="lime" stroke="black" stroke-width="5"/>
	
	<path d="M25 470 L150 350 L200 420 Z" fill="red" stroke="black" stroke-width="5"/>
	<path d="M 240 400 q 100 -130 200 40" stroke="blue" stroke-width="5" fill="none" />
	
	<text x="480" y="420" font-size="72">Text</text>
</svg>


// Path
<path>

// Positioning
<svg xmlns="http://www.w3.org/2000/svg"> //absolute
	<circle cx="75" cy="75" r="50" fill="blue" />
</svg>

<svg xmlns="http://www.w3.org/2000/svg"> //relative to viewpoint
	<circle cx="50%" cy="50%" r="25%" fill="green" />
</svg>
```
### Path
#### Turtle Graphics for Paths
- Linear movements (see previous page)
- Arcs
- Bézier curves

![[Pasted image 20240930161505.png#invert]]
![[Pasted image 20240930161515.png#invert]]
#### Path Description

<svg xmlns="http://www.w3.org/2000/svg">
<path stroke="orange" stroke-width="5" fill="yellow" d="M 40,180
V 80
l 40,-40
q 50,-50 150,0 40,20 60,0
l 90,60
V 180
z" />
</svg>
### Groups

#### Reference Id
```html
<g id=“myGroup1“> … </g>
```
#### Shared Transformation
```html
<g id=“myGroup1" transform="translate(200 100)"> … </g>
```
![[Pasted image 20240930161820.png#invert]]
![[Pasted image 20240930161826.png#invert]]
#### Combined Transformation
<svg width="300" height="300" style="border: 1px solid #CCCCCC">
	<rect width="50" height="20" />
	<rect width="50" height="20" transform="translate(150 25)"/>
	<rect width="50" height="20" transform="translate(50 50) scale(2 1) rotate(45 25,5)"
	/>
	<rect width="50" height="20" transform="rotate(45 25,5) scale(2 1) translate(50 50)"
	/>
</svg>
### Text
#### Styling
<svg xmlns="http://www.w3.org/2000/svg"
width="340px" height="240px">
<text x="20" y="40"
transform="rotate(30 20,40)"
style="font-family: Times New Roman;
font-size : 48;
stroke : #ff0000;
fill : #ffbb00;">
SVG Text Styling
</text>
</svg>
#### Inline
```html
<body>
<H1>SVG code embedded inline in HTML</H1>
<br>
<svg height="200" width="500">
<ellipse cx="200" cy="100" rx="100" ry="75" fill=“blue" />
Sorry, your browser does not support inline SVG.
</svg>
</body>
```
## SVG vs. Canvas
![[Pasted image 20250113200332.png]]
