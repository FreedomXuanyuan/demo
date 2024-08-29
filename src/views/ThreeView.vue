<template>
  <div id="threejs-container"></div>
</template>

<script>
import * as THREE from 'three';
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader';

export default {
  name: 'ThreeJsFbxModel',
  mounted() {
    const container = document.getElementById('threejs-container');
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(container.clientWidth, container.clientHeight);
    container.appendChild(renderer.domElement);

    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0xbfe3dd);

    const camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 1, 10000);
    camera.position.set(0, 100, 800);

    const ambientLight = new THREE.AmbientLight(0x666666);
    scene.add(ambientLight);

    const directionalLight = new THREE.DirectionalLight(0xdfebff, 0.5);
    directionalLight.position.set(50, 200, 100);
    scene.add(directionalLight);

    const loader = new FBXLoader();
    loader.load('/models/beijing.fbx', (fbx) => {
      fbx.scale.set(10.01, 10.01, 10.01); // 根据需要调整模型大小
      fbx.traverse((child) => {
        if (child.isMesh) {
          child.castShadow = true;
        }
      });
      scene.add(fbx);

      function animate() {
        requestAnimationFrame(animate);
        renderer.render(scene, camera);
      }

      animate();
    }, (xhr) => {
      console.log((xhr.loaded / xhr.total * 100) + '% loaded');
    }, (error) => {
      console.error('An error happened', error);
    });
  }
};
</script>

<style>
#threejs-container {
  width: 100%;
  height: 100vh;
}
</style>