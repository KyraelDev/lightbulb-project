<template>
    <div id="container" ref="container"></div>
  </template>
  
  <script>
  import * as THREE from 'three';
  import { PointerLockControls } from 'three/examples/jsm/controls/PointerLockControls';
  
  export default {
    data() {
      return {
        controls: null,
        scene: null,
        camera: null,
        renderer: null,
      };
    },
    mounted() {
      this.initScene();
      this.initControls();
      this.animate();
  
      this.$refs.container.addEventListener('click', () => {
        this.controls.lock();
      });
  
      // Remove event listeners to prevent memory leaks
      window.addEventListener('unload', this.cleanUpThreeJS);
      window.addEventListener('beforeunload', this.cleanUpThreeJS);
    },
    methods: {
        initScene() {
      this.scene = new THREE.Scene();
      const geometry = new THREE.BoxGeometry(10, 10, 10);
      const material = new THREE.MeshBasicMaterial({ color: 0xffffff });
      const cube = new THREE.Mesh(geometry, material);
      this.scene.add(cube);

      this.camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      this.camera.position.z = 20;

      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.$refs.container.appendChild(this.renderer.domElement);
    },
    initControls() {
      this.controls = new PointerLockControls(this.camera, this.$refs.container);
      this.scene.add(this.controls.getObject());
    },
    animate() {
      requestAnimationFrame(this.animate);
      if (this.controls) {
        this.controls.update();
      }
      this.renderer.render(this.scene, this.camera);
    },
    cleanUpThreeJS() {
      // Dispose renderer resources to release memory
      this.renderer.dispose();

      // Additional cleanup code, e.g., removing objects from the scene

      // Remove event listeners to avoid memory leaks
      window.removeEventListener('unload', this.cleanUpThreeJS);
      window.removeEventListener('beforeunload', this.cleanUpThreeJS);
    }
  },
};
</script>

<style>
  /* Optional style for the container */
  #container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }
</style>
