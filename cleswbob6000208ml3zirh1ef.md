---
title: "Code Structuring for Creative Coding"
datePublished: Fri Mar 03 2023 18:55:44 GMT+0000 (Coordinated Universal Time)
cuid: cleswbob6000208ml3zirh1ef
slug: code-structuring-for-creative-coding
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1677593613407/c5c86503-62fb-4c62-b3e7-9b4b65f0b744.png
tags: tutorial, webgl, threejs, creative-coding, reactthreefiber

---

When you're starting out with three.js, your projects might be simple enough to fit into a single JavaScript file. But as you take on more complex projects, you'll quickly realize that having everything tangled up like spaghetti in one file is a recipe for disaster.

Sure, you can use block comments to separate different parts of your code, but let's face it - you'll still need to scroll through a lot of code to find what you're looking for. And that's just the tip of the iceberg 🤯

Think about it: it's hard to find what you want when everything's jumbled together. It's even harder to reuse specific parts of your code, and you constantly have to worry about variable conflicts. And if you're working with other developers, forget about it - you'll be dealing with conflicts left and right.

Plus, let's not forget the physical toll it takes on you. Your fingers will start to cramp up from all that scrolling. *And who wants that? 👀*

We need to structure our code in a more maintainable way. Don't worry, it's not as daunting as it sounds. By breaking your code up into smaller, more manageable pieces, you'll make it easier to navigate and maintain in the long run.

Trust me, your fingers (and your fellow developer friends) will thank you for it.

## Modules

When it comes to organizing our code, modules are a game-changer. The basic concept is to divide our code into multiple files, so that we can import and use only what we need, when we need it.

In fact, if you've ever imported dependencies into your code, you're already familiar with how modules work. It's a simple yet powerful way to keep your codebase neat and tidy, and avoid cluttering your files with code that you don't need right away.

By breaking down the code down into smaller, more focused chunks, we'll be able to make our code easier to read, maintain, and scale as the project grows.

```javascript
import * as THREE from 'three'
import gsap from 'gsap'
```

## Syntax

We are going to ignore the current state of our project for a moment to focus on syntax.

In `/src/script.js`, comment out everything (even the CSS import).

In the `/src/` folder, create a `cool.js` file. We are going to add content to that file and import it into `script.js`.

A file can export one or multiple things, but, to keep things simple, I like to export only one thing per file.

To do that, write the following code in `cool.js` :

```javascript
export default 'Hello developer friend!'
```

And then, to import this code into `/src/script.js`, write the following code:

```javascript
import test from './cool.js'

console.log(test)
```

And that's it. Check your console and you should see `Hello developer friend!`.

One very important detail is that the path starts with `./`. When we refer to a file, we need to do it that way, otherwise the build tool will try to find it in the `node_modules` folder.

Here, we exported a string, which is not very useful. But we can export functions:

```javascript
// cool.js
export default () =>
{
    console.log('Hello developer friends')
}

// scripts.js
import test from './cool.js'

test()
```

We can also export objects:

```javascript
// test.js
export default {
    hello: 'modules'
}

// scripts.js
import test from './cool.js'

console.log(test)
```

And we can also export classes, but we are going to see that later.

The `export` instruction can also be done after the object:

```javascript
// test.js
const somethingToExport = {
    hello: 'modules'
}

export default somethingToExport
```

And as mentioned earlier, one file can export multiple things:

```javascript
// test.js
const oneThing = {
    hello: 'modules'
}

const anotherThing = () =>
{
    console.log('Hi!')
}

export { oneThing, anotherThing }

// scripts.js
import { oneThing, anotherThing } from './cool.js'

console.log(oneThing)
anotherThing()
```

By exporting multiple things, we don't need to import everything in the module. We can select what we want:

```javascript
// script.js
import { oneThing } from './cool.js'

console.log(oneThing)
```

And this is actually how Three.js classes can be imported without importing the whole library.

Currently, when we import Three.js, we do:

```javascript
import * as THREE from 'three'
```

And everything that is being exported from `three` will be available in the `THREE` variable. But we can choose to import specific classes like this:

```javascript
import { SphereGeometry } from 'three'
```

But again, we are not going to use that feature and each one of our files is going to export only one thing.

### **Inheritance**

Inheritance is like creating a class based on another class. In a way, we create a blueprint based on another blueprint.

All the methods of the base class will be available in the new class.

To illustrate that, let's add a feature to our robots so that they can fly. But not every robot can fly like Wall-E. Still, every robot needs a name and legs.

To create a class based on another, use the `extends` keyword. Create the following class after the `Robot` class:

```javascript
class FlyingRobot extends Robot
{
    
}
```

We have created a `FlyingRobot` class which we can now use for robots that can fly:

```javascript
const wallE = new Robot('Wall-E', 0)
const ultron = new FlyingRobot('Ultron', 2)
const astroBoy = new FlyingRobot('Astro Boy', 2)
```

Currently, this `FlyingRobot` doesn't add anything to the `Robot` class, but we can add methods like this:

```javascript
class FlyingRobot extends Robot
{
    takeOff()
    {
        console.log(`Have a good flight ${this.name}`)
    }

    land()
    {
        console.log(`Welcome back ${this.name}`)
    }
}
```

Robots instantiated with `FlyingRobot` will still be able to say "hi", but now they will also be able to take off and land:

```javascript
astroBoy.sayHi()
astroBoy.takeOff()
astroBoy.land()
```

But if we try to do the same with Wall-E:

```javascript
wallE.takeOff()
```

We get an error. Wall-E isn't an instance of `FlyingRobot` and thus can't take off.

Providing a method with the same name to the `FlyingRobot` class will override what the method does in the `Robot` class:

```javascript
class FlyingRobot extends Robot
{
    sayHi()
    {
        console.log(`Hello! My name is ${this.name} and I am a flying robot`)
    }

    // ...
}
```

But if you want to provide a different `constructor`, you have to start the method with `super()` and send the needed parameters to it:

```javascript
class FlyingRobot extends Robot
{
    constructor(name, legs)
    {
        super(name, legs)

        this.canFly = true
    }

    // ...
}
```

`super` corresponds to the base class (`Robot`) and using `super()` is like calling the base `constructor` so that everything we do in the base constructor will be done in the new class, too.

We can also use `super` to call methods from the base class. As an example, we can make the robot say "hi" like it use to and then, in another log, say that it is a flying robot:

```javascript
class FlyingRobot extends Robot
{
    sayHi()
    {
        super.sayHi()

        console.log('I am a flying robot')
    }

    // ...
}
```

**Note:** this approach tends to complicate the code, don't overuse it.

## **Combining the classes and the modules**

The idea here is that we are going to separate our code into files and each one of these files will export a different class.

To illustrate that with the robots, create a `/src/Robot.js` file and put the `Robot` class in it, but with an `export default` at the beginning:

```javascript
export default class Robot
{
    constructor(name, legs)
    {
        this.name = name
        this.legs = legs

        console.log(`I am ${this.name}. Thank you creator`)

        this.sayHi()
    }

    sayHi()
    {
        console.log(`Hello! My name is ${this.name}`)
    }
}
```

Now create a `/src/FlyingRobot.js` file and put the `FlyingRobot` class in it, but with an `export default` at the beginning:

```javascript
export default class FlyingRobot extends Robot
{
    constructor(name, legs)
    {
        super(name, legs)

        this.canFly = true
    }

    sayHi()
    {
        console.log(`Hello! My name is ${this.name} and I'm a flying robot`)
    }

    takeOff()
    {
        console.log(`Have a good flight ${this.name}`)
    }

    land()
    {
        console.log(`Welcome back ${this.name}`)
    }
}
```

Before importing them, however, we need to fix an issue.

`FlyingRobot` inherits from `Robot`, but `Robot` isn't available in the file. We need to first import that class to refer to it.

Add the following import:

```javascript
import Robot from './Robot.js'

export default class FlyingRobot extends Robot
{
    // ...
```

In `/src/scripts.js`, we can now import and use these classes:

```javascript
import Robot from './Robot.js'
import FlyingRobot from './FlyingRobot.js'

const wallE = new Robot('Wall-E', 0)
const ultron = new FlyingRobot('Ultron', 2)
const astroBoy = new FlyingRobot('Astro Boy', 2)
```

And our code to create robots becomes suddenly very simple.

At first, all of this might seem a bit complicated, but your code will become much more maintainable and you'll be able to reuse it in different projects simply by copying the classes you need.

## Structuring a Creative Project

A good practice is to put the whole experience inside a main class that will then create everything else. This is particularly useful if your WebGL experience is part of a bigger website with HTML content, other pages, etc.

The code related to your experience will be separate from the rest of your code, but still accessible through the class and all the methods and properties you provide within that class.

As for the name of that class, I like to use `Experience` but it can be `MySuperGame`, `WebGLAwesomeStuff`, `Application` or whatever.

### **Create and instantiate the class**

In the `/src/` folder, create an `Experience/` folder and, in that `/src/Experience` folder, create an `Experience.js` file.

In that file, export a class as follows:

```javascript
export default class Experience
{
    constructor()
    {
        console.log('Here starts a great creative experience')
    }
}
```

All classes related to the experience will be in that folder.

In `/src/script.js`, we can import and instantiate that class:

```javascript
import Experience from './Experience/Experience.js'

const experience = new Experience()
```

### **Canvas**

Covering the canvas as our example for this article, is good to know that when instantiating the Experience, we are going to send the canvas as a parameter so that other developers using our class in different situations will be able to choose what `<canvas>` they want to use.

When instantiating in `/src/script.js`, use `querySelector()` to send the canvas parameter:

```javascript
const experience = new Experience(document.querySelector('canvas.webgl'))
```

And, in the class, save it as a property:

```javascript
export default class Experience
{
    constructor(canvas)
    {
        // ...

        // Options
        this.canvas = canvas
    }
}
```

### **Sizes**

The first and super useful class we will cover in this article is the one that will handle the sizes of the experience. It'll include the width and the height of the viewport as well as the pixel ratio of the screen.

We are going to update these values when a resize occurs, but we are also going to warn the experience of that resize.

In the `/src/Experience/Utils/` folder, create the `Sizes.js` class:

```javascript
export default class Sizes
{
    constructor()
    {
    }
}
```

And instantiate it in the `Experience` class:

```javascript
import Sizes from './Utils/Sizes.js'

export default class Experience
{
    constructor(canvas)
    {
        // ...

        // Setup
        this.sizes = new Sizes()
    }
}
```

In that `Sizes` class, add the usual `width`, `height` and `pixelRatio` as we did before, but save them as properties:

```javascript
export default class Sizes
{
    constructor()
    {
        // Setup
        this.width = window.innerWidth
        this.height = window.innerHeight
        this.pixelRatio = Math.min(window.devicePixelRatio, 2)
    }
}
```

Then listen to the resize event and update those properties:

```javascript
export default class Sizes
{
    constructor()
    {
        // ...

        // Resize event
        window.addEventListener('resize', () =>
        {
            this.width = window.innerWidth
            this.height = window.innerHeight
            this.pixelRatio = Math.min(window.devicePixelRatio, 2)
        })
    }
}
```

Here, we assume that the experience always fills the viewport. If that's not the case, you'll have to do things differently.

We can now access the `width`, `height` and `pixelRatio` from the `Experience` class:

```javascript
import Sizes from './Utils/Sizes.js'

export default class Experience
{
    constructor(canvas)
    {
        // ...

        this.sizes = new Sizes()

        console.log(this.sizes.width)
        console.log(this.sizes.height)
        console.log(this.sizes.pixelRatio)
    }
}
```

At some point, we will also have to update other values like the camera or the renderer when a resize occurs. We could listen to the `resize` event on `window` like we just did, but instead, we are going to use the `Sizes` class to warn the other classes about that change.

## Closing thoughts

If you're working on a Three.js or React Three.js project, you already know that these libraries offer a lot of flexibility and power when it comes to creating 3D visualizations, animations, and interactive experiences. But with great power comes great responsibility, especially when it comes to organizing your code. Here are some tips to help you structure your code in a way that's clear, efficient, and maintainable.

1. Start with a plan: Before you dive into coding, take some time to sketch out your project's architecture and flow. Think about the different components or modules you'll need, and how they'll interact with each other. Consider using a diagramming tool like Lucidchart or [Draw.io](http://Draw.io) to visualize your plan.
    
2. Break it down into components: In React Three.js, everything is a component. Take advantage of this by breaking your code down into small, reusable components that do one thing and do it well. This makes it easier to manage your code, test your components in isolation, and swap out components as needed.
    
3. Use a folder structure: Create a folder structure that makes sense for your project, and stick to it. For example, you might have separate folders for components, utilities, assets, and tests. This helps you find what you need quickly, and keeps your project organized as it grows.
    
4. Name your files and components clearly: Choose descriptive names for your files and components, and avoid using generic names like "utils" or "helpers". This makes it easier to understand what each file or component does, and helps you avoid naming collisions with other libraries or modules.
    
5. Use a linter: A linter is a tool that checks your code for style and syntax errors, and can also enforce coding standards and best practices. Use a linter like ESLint or Prettier to keep your code consistent and readable, and catch errors before they cause problems.
    
6. Use version control: Whether you're working solo or with a team, version control is essential for managing changes to your code over time. Use a version control system like Git to track changes, collaborate with others, and revert to earlier versions if needed.
    
7. Keep your code DRY: DRY stands for "Don't Repeat Yourself", and it's a fundamental principle of good code design. Avoid duplicating code across your project, and instead look for ways to abstract common functionality into reusable functions or modules.
    
8. Use comments judiciously: Comments can be helpful for explaining complex code or providing context for others who might work on your project. But too many comments can clutter your code and make it harder to read. Use comments sparingly, and focus on writing code that's self-explanatory.
    
9. Test your code: Finally, make sure to test your code thoroughly to catch errors and ensure that your project works as expected. Use a testing framework like Jest or Enzyme to write unit tests for your components and utilities, and automate your tests using tools like Travis CI or CircleCI.
    

By following these tips, you'll be well on your way to writing clean, organized code that's easy to maintain and build upon over time.

Remember, good code structure isn't just a nicety - it's essential for creating successful Three.js or React Three.js projects that meet your goals and exceed your users' expectations.

---

That is it for this article about structuring big creative projects!

Let's connect on [**Twitter**](https://twitter.com/danizeres) and [**LinkedIn**](https://www.linkedin.com/in/danipassos/) 👋