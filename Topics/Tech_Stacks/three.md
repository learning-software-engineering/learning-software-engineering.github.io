
# Creating Your First Scene and 3D Object with Three.js

This tutorial will guide you through the process of creating your first scene and 3D object using Three.js, a JavaScript library that simplifies the use of WebGL for 3D graphics in a web browser. In order to do this, you'll need: 

-   Basic understanding of HTML, CSS, and JavaScript
-   A browser that supports WebGL
-   Any text / code editor

## Setting Up Your Files

To discuss how to creating a functioning scene in Three.js and render your first 3D object, we can examine some code excerpts from the Three.js documentation.

First, you will need to create a new HTML file named `index.html` 

```html
<!DOCTYPE html>  
<html  lang="en">  
	<head>  
		<meta  charset="utf-8">  
		<title>My first three.js app</title>  
		<style> 
			body { margin:  0;  }  
		</style>  
	</head>  
	<body>  
		<script  type="module"  src="/main.js"></script>  
	</body>  
</html>
```

Next, create a JavaScript file `main.js`, make sure to import the Three.js library.

```javascript
// Imports the Three.js library
import  *  as THREE from  'three';  
```

## Creating the Scene

Now that you have your JavaScript file, you'll have to create the scene, camera, and renderer.

```javascript
// Creates the scene and camera
const scene =  new THREE.Scene();  
const camera =  new THREE.PerspectiveCamera(  75, window.innerWidth / window.innerHeight,  0.1,  1000  );  

// Creates the renderer and appends it to the parent HTML document
const renderer =  new THREE.WebGLRenderer(); 
renderer.setSize( window.innerWidth, window.innerHeight ); 
document.body.appendChild( renderer.domElement );
```


- Scene: A scene holds all your objects, cameras, and lights in Three.js.

- Camera: Defines the POV from which you'll see the scene. It contains the attributes (`field of view`, `aspect ratio`, `near`, `far`). In the example, these attributes are set to ( 75, window.innerWidth / window.innerHeight,  0.1,  1000 ) respectively. 

- Renderer: Renders the graphics onto the screen. In the example, the function `renderer.setSize()` sets the size of the renderer to be the same as the display window before `document.body.appendChild()` adds it to the HTML document. 

## Creating and Rendering Your First 3D Object

Now that we have our scene, camera, and renderer, we can get started with creating and animating our first 3D object.

We can do this through the following code excerpt.

```javascriptCopy 
// Creates a cube and adds it to the scene
var geometry = new THREE.BoxGeometry(1, 1, 1); // Width, Height, Depth
var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
var cube = new THREE.Mesh(geometry, material);
scene.add(cube);

// Animates the cube and renders it through the renderer
function animate() {
    requestAnimationFrame(animate);

    // Rotate the cube
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;

    renderer.render(scene, camera);
}

animate();` 
```

In order to create a 3D object, in this case a cube, we initialize a `BoxGeometry` with vertices (1, 1, 1). The cube's material, or texture in other words, is set to be `MeshBasicMaterial`, one of the standards that Three.js comes with, and it's colour is set to `0x00ff00`. 

We then use `Mesh` to combine the `geometry`, the desired geometrical shape of our object with `material`, the desired texture and colour of our 3D object to create a cube. After which `scene.add()`
adds the initialized cube to the scene we created in the previous section. 

Now, in order to make the cube appear, we create the `animate()` function, which uses `requestAnimationFrame()` to draw the cube onto the scene during every refresh, and `renderer.render()` to actually render the cube.

Additionally, changing `cube.rotation.x` and `cube.rotation.y` on every frame refresh gives the effect of the cube rotating on its x and y axis.

Now all you have to do is open `index.html` in a WebGL-compatible web browser to see your scene. You should see a rotating green cube against a black background.

## Reasons to consider Three.js

Three.js is a simple yet powerful tool that makes creating 3D graphics on the web easy and accessible. It allows people to build and manipulate 3D scenes without extensive knowledge of WebGL, which is complex and can be very daunting for many beginners. This makes it a very valuable tool that opens up many opportunities  for anyone that is considering venturing into the world of 3D design and web development. 


## References
- https://threejs.org/docs/#manual/en/introduction/Creating-a-scene

