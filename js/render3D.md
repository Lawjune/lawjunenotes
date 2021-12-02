## 1. Download js files
https://raw.githubusercontent.com/mrdoob/three.js/dev/build/three.js

https://github.com/mrdoob/three.js/blob/dev/examples/js/controls/OrbitControls.js

https://github.com/mrdoob/three.js/blob/dev/examples/js/loaders/GLTFLoader.js

## 2. Download the 3D models

https://sketchfab.com/jimmyn64/collections/downloadable-cars

## 3. Basic Setup

*Create a sscene, camera and renderer. I’m going to place the camera in front of the car and rotate them by 45 degrees.*

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" type="text/css" href="./css/styles.css" />
  </head>
  <body>
    <script src="./js/three.js"></script>
    <script src="./js/GLTFLoader.js"></script>
    <script src="./js/OrbitControls.js"></script>
    <script>
      let scene, camera, renderer;

      function init() {
        renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.gammaOutput = true;
        renderer.gammaFactor = 2.2;
        document.body.appendChild(renderer.domElement);

        scene = new THREE.Scene();
        scene.background = new THREE.Color(0xdddddd);

        camera = new THREE.PerspectiveCamera(
          40,
          window.innerWidth / window.innerHeight,
          1,
          5000
        );
        camera.rotation.y = (45 / 180) * Math.PI;
        camera.position.x = -4;
        camera.position.y = 2;
        camera.position.z = -5;
      }

      init();
    </script>
  </body>
</html>
```

## 4. The Lighting

*Then I’ll add a soft white ambient light to illuminate the scene globally.*

*Then add directional light from above. I’m going to set the castShadow property to true then add it to the scene. I’m going to also add 4 point lights and place them around the car. Point light is similar to the light bulb in the real world and It automatically cast shadow.*

```js
        var hemiLight = new THREE.HemisphereLight(0xffffff, 0x444444);
        hemiLight.position.set(0, 20, 0);
        scene.add(hemiLight);

        var dirLight = new THREE.DirectionalLight(0xffffff);
        dirLight.position.set(-3, 10, -10);
        dirLight.castShadow = true;
        dirLight.shadow.camera.top = 2;
        dirLight.shadow.camera.bottom = -2;
        dirLight.shadow.camera.left = -2;
        dirLight.shadow.camera.right = 2;
        dirLight.shadow.camera.near = 0.1;
        dirLight.shadow.camera.far = 40;
        scene.add(dirLight);
```

## 5. Loading Model

*We’ll use three.js OrbitControl plugin to add a 360 degrees viewer that let the users rotate the camera. Get the OrbitControls.js from github and include it to the page.*