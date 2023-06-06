---
title: "Create an Interactive Three.js Scene"
seoTitle: "Make an Interactive Three.js Scene"
seoDescription: "Create an interactive Three.js scene with rotating squares that change color when hovered over in this tutorial."
datePublished: Tue Mar 21 2023 20:07:59 GMT+0000 (Coordinated Universal Time)
cuid: clfiotxs2000009lbfbpm8ffc
slug: create-an-interactive-threejs-scene
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679429130170/e9592473-577e-4e4c-b684-6d8cc0b0c205.png
tags: tutorial, webgl, web-development, threejs

---

Three.js is an awesome library that simplifies 3D graphics rendering using WebGL. In this tutorial, I will walk you through creating a responsive Three.js scene with two interactive squares that rotate around the Z-axis. When you hover your mouse over them, their color changes. By the end of this article, you'll have a good understanding of setting up a Three.js project, creating and animating objects, and handling user interaction.

Let's dive in! 👇

### Step 1: Setting up the project

We'll use [CodeSandbox](http://Codesandbox.io) for this tutorial. It's an online code editor that makes it easy to create and share web projects. Create a new "Vanilla" project, add `three` as a dependency, and add a new file called "index.html" with the following content:

```xml
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Interactive Three.js Squares</title>
  </head>
  <body>
    <script src="index.js"></script>
  </body>
</html>
```

### Step 2: Importing Three.js

Add a new file called "index.js" and import the Three.js library using Skypack:

```javascript
import * as THREE from "three";
```

### Step 3: Creating the scene, camera, and renderer

To start, we'll create a new Three.js scene, a perspective camera, and a WebGL renderer. We'll set the renderer's size to match the window's size and append its DOM element to the body:

```javascript
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 5;

const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```

### Step 4: Creating the materials and squares

Next, we'll create two materials: one teal and one pink. We'll also create a helper function to generate squares with the specified position and material:

```javascript
const teal = new THREE.MeshStandardMaterial({ color: "#BADAFF" });
const pink = new THREE.MeshStandardMaterial({ color: "#FFADED" });

const createSquare = (x, y, material) => {
  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const square = new THREE.Mesh(geometry, material);
  square.position.set(x, y, 0);
  square.rotation.z = THREE.MathUtils.degToRad(15);
  scene.add(square);
  return square;
};

const square1 = createSquare(-2, 0, teal.clone());
const square2 = createSquare(2, 0, teal.clone());
```

### Step 5: Handling mouse interaction

To make the squares change color when the mouse hovers over them, we'll need a `Raycaster`. A `Raycaster` is used for picking objects in the scene by casting a ray and checking for intersections with objects. We'll also need a `Vector2` object to store the mouse coordinates.

```javascript
const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();
```

Next, create an event listener for the `mousemove` event. This event will update the `mouse` object's x and y coordinates when the mouse moves.

```javascript
const onMouseMove = (event) => {
  event.preventDefault();
  mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
  mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;
};

window.addEventListener("mousemove", onMouseMove, false);
```

### Step 6: Add lights to the scene

Now, let's add a `PointLight` and an `AmbientLight` to the scene to make the squares look more three-dimensional.

```javascript
const pointLight = new THREE.PointLight(0xffffff, 1, 100);
pointLight.position.set(0, 0, 10);
scene.add(pointLight);

const ambientLight = new THREE.AmbientLight(0x404040);
scene.add(ambientLight);
```

### Step 7: Make the page responsive

To make the page responsive, add an event listener for the `resize` event. This event will update the camera's aspect ratio and the renderer's size when the window is resized.

```javascript
const onWindowResize = () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
};

window.addEventListener("resize", onWindowResize, false);
```

### Step 8: Animate the scene

In the `animate` function, we'll use the `raycaster` to detect if the mouse is hovering over any of the squares. If so, we'll change the color of the intersected squares to pink.

Also, let's make the squares spin slowly around the Z-axis.

```javascript
function animate() {
  requestAnimationFrame(animate);

  raycaster.setFromCamera(mouse, camera);
  const intersects = raycaster.intersectObjects([square1, square2]);

  square1.material = teal.clone();
  square2.material = teal.clone();

  for (const intersect of intersects) {
    intersect.object.material = pink.clone();
  }

  square1.rotation.z += 0.01;
  square2.rotation.z += 0.01;

  renderer.render(scene, camera);
}

animate();
```

And that's it! You've successfully created a simple, interactive Three.js scene with two spinning squares that change color when the mouse hovers over them.

Now you can experiment with different shapes, colors, and interactions to create even more engaging 3D scenes 🔥

---

That is it for this article!

Let's connect on [**Twitter**](https://twitter.com/danizeres) and [**LinkedIn**](https://www.linkedin.com/in/danipassos/) 👋