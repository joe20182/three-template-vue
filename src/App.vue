<script setup lang="ts">
import { onMounted } from "vue";
import * as Three from "three";
import * as dat from "dat.gui";

const vp = {
  width: window.innerWidth,
  height: window.innerHeight,
};

new dat.GUI();

onMounted(() => {
  const canvas = document.querySelector("#canvas");

  const renderer = new Three.WebGLRenderer({ antialias: true });
  renderer.setPixelRatio(Math.min(2, window.devicePixelRatio));
  renderer.setSize(vp.width, vp.height);
  canvas?.appendChild(renderer.domElement);

  const scene = new Three.Scene();

  const camera = new Three.PerspectiveCamera(
    75,
    vp.width / vp.height,
    0.1,
    1000
  );
  camera.position.z = 5;

  const box = new Three.Mesh(
    new Three.BoxGeometry(),
    new Three.MeshNormalMaterial()
  );
  scene.add(box);

  const animate = () => {
    requestAnimationFrame(animate);
    renderer.render(scene, camera);

    box.rotation.x += 0.01;
    box.rotation.y += 0.01;
  };

  animate();
});
</script>

<template>
  <div id="canvas"></div>
</template>
