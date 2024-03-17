 ## Table of Contents
 - [Installation](installation)
 - [Option 1: NPM and build tool](option-1)
 - [Option 2: Import from CDN](option-2)
 - [Addons](addons)
 - [References](references)
   
<a name="installation"></a># Installation
You will need:
- One html file
- Javascript file with `import * as THREE from 'three';` at the top
- public/ folder. This is also known as a static folder, and will usually contain textures, audio, and 3D models.
  
<a name="option-1"></a>## Option 1 for installation: NPM and build tool (recommended approach)
1. Install node.js
   We will use this to load and manage dependencies and to run the build tool.
2. Install three.js and a build tool such as Vite through a terminal in your project folder.
   `three.js npm install --save three` Installs three.js.
   `npm install --save-dev vite` Installs Vite. You may use another build tool if you wish.
3. From the terminal, run:
   `npx vite`

Result: You should see a URL such as http://localhost:5173 appear in the terminal, which you can click on to open up the webpage. The page will start off as blank until you create a scene.
When you are ready to deploy your web app, use Vite to run a production build using `npx vite build` in the terminal. Everything used by the app will be copied into the dist/ folder, which will contain everything that can be hosted on your website. 

<a name="option-2"></a>## Option 2 for installation: Import from a CDN
Installing without build tools will change your project structure.

1. We previously imported code from the npm package 'three' in the javascript file. Web browsers don't understand what that means, so in the html file we will need to add an import
   map defining where to get the package. Put the following code inside the <head></head> tag, after the styles. Replace <version> with an actual version of three.js, a list of which can be found here:
   https://www.npmjs.com/packagethree?activeTab=versions
```html
<script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@<version>/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@<version>/examples/jsm/"
    }
  }
</script>
```
﻿2. We will also need to run a local server, so the web browser can access these files at a URL. Install Node.js then run the following command in a terminal to start a local server 
   in the project directory.
   `npx serve .`

Result: You should see a URL like http://localhost:3000 appear in your terminal, which you can open to see your web app. This page will start off as blank until you create a scene. When you are ready to deploy your web app, push the source files to your web hosting provider. You will need to keep the import map updated with any dependencies that your app requires. If the CDN hosting your dependencies goes down, your website will go down too.
Importantly, make sure to import all dependencies from the same version of three.js and from the same CDN. Mixing files from different sources may cause duplicate code to be included, or break the application.

<a name="addons"></a>## Addons:
Certain three.js components, such as controls, loaders, and post-processing effects, are a part of the addons/ directory. Addons need to be imported separately. here is an example of importing some addons:
```javascript
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';

const controls = new OrbitControls( camera, renderer.domElement );
const loader = new GLTFLoader();
```

<a name="references"></a># References
https://threejs.org/docs/#manual/en/introduction/Installation
