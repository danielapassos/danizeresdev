---
title: "The Ultimate Guide to React Three Fiber: How to Set Up Your Development Environment"
seoTitle: "React Three Fiber: Setting Up Your Environment"
seoDescription: "Learn how to set up your development environment for React Three Fiber with this ultimate guide. Install Node.js, npm, create-react-app, and more"
datePublished: Tue Mar 14 2023 19:10:06 GMT+0000 (Coordinated Universal Time)
cuid: clf8moisg00040akthsv31ztu
slug: the-ultimate-guide-to-react-three-fiber-how-to-set-up-your-development-environment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678820952408/4a87cf12-d092-4e14-9296-7f68834e7197.png
tags: creativity, threejs, creative-coding, reactthreefiber

---

In this tutorial, I will walk you through setting up your development environment for React Three Fiber. We'll cover the importance of each tool, including Node.js, npm, and create-react-app.

Prerequisites: Before we start, ensure that you have the following installed on your computer:

1. Node.js (version 12 or higher): You can download it from [**https://nodejs.org/en/download/**](https://nodejs.org/en/download/)
    
2. npm (version 6 or higher): It comes bundled with Node.js, so you don't need to install it separately.
    

### Step 1: Installing create-react-app

To get started with React Three Fiber, we'll use create-react-app, a popular boilerplate for creating React applications. To install it globally on your computer, open your terminal or command prompt and run the following command:

```plaintext
npm install -g create-react-app
```

### Step 2: Creating a new React project

Now that we have create-react-app installed, let's create a new React project. Run the following command to generate a new project called "react-three-fiber-demo":

```plaintext
create-react-app react-three-fiber-demo
```

Once the project is created, navigate to the project folder:

```plaintext
cd react-three-fiber-demo
```

### Step 3: Installing React Three Fiber and Three.js

React Three Fiber is built on top of Three.js, so we need to install both libraries. Run the following command to add them to your project:

```plaintext
npm install three react-three-fiber
```

### Step 4: Creating a basic React Three Fiber scene

Now, let's create a basic React Three Fiber scene. Open "src/App.js" in your favorite code editor and replace its content with the following code:

```plaintext
import React from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls, Box } from '@react-three/drei';

function App() {
  return (
    <div style={{ height: '100vh', width: '100vw' }}>
      <Canvas>
        <ambientLight intensity={0.5} />
        <pointLight position={[10, 10, 10]} />
        <Box position={[-1.2, 0, 0]}>
          <meshStandardMaterial color={'orange'} />
        </Box>
        <Box position={[1.2, 0, 0]}>
          <meshStandardMaterial color={'blue'} />
        </Box>
        <OrbitControls />
      </Canvas>
    </div>
  );
}

export default App;
```

In this code, we import React, the Canvas component from React Three Fiber, and the OrbitControls and Box components from the '@react-three/drei' package, which provides useful utilities and components for working with React Three Fiber.

We then create a simple scene with two 3D boxes and some lights. The OrbitControls component allows us to navigate around the scene using the mouse.

### Step 5: Running the development server

To see your React Three Fiber scene in action, start the development server by running the following command in the terminal:

```plaintext
npm start
```

Your browser should open automatically and display the React Three Fiber scene.  
If it doesn't, open your browser and go to [**http://localhost:3000/**](http://localhost:3000/).

Congratulations! You have successfully set up your development environment for React Three Fiber and created a basic 3D scene. You can now start exploring more advanced concepts and create amazing projects.

---

That is it for this article!

Let's connect on [**Twitter**](https://twitter.com/danizeres) and [**LinkedIn**](https://www.linkedin.com/in/danipassos/) 👋