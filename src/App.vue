<template>
  <Renderer ref="renderer" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
    <Camera :position="{ z: 10 }" />
    <Scene>
      <PointLight :position="{ y: 50, z: 50 }" />
      <Box :size="1" ref="box" :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }">
        <LambertMaterial />
      </Box>
      <Capsule>
        <LambertMaterial />
      </Capsule>

      <CannonWorld :gravity="{ x: 0, y: -9.82, z: 0 }" @before-step="onBeforeStep">

      </CannonWorld>
    </Scene>
  </Renderer>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { Box, Camera, LambertMaterial, MeshPublicInterface, PointLight, Renderer, RendererPublicInterface, Scene, Capsule } from './export'
import CannonWorld from "./components/physics/CannonWorld.js";


//import { Box, Camera, LambertMaterial, MeshPublicInterface, PointLight, Renderer, RendererPublicInterface, Scene, Capsule } from '../build/trois.module'

export default defineComponent({
  components: { Box, Camera, LambertMaterial, PointLight, Renderer, Scene, Capsule, CannonWorld },
  mounted() {
    const renderer = this.$refs.renderer as RendererPublicInterface
    const mesh = (this.$refs.box as MeshPublicInterface).mesh
    if (renderer && mesh) {
      renderer.onBeforeRender(() => {
        mesh.rotation.x += 0.01
      })
    }
  },
  methods:{
    onBeforeStep() {
    }
  }
})
</script>

<style>
body, html {
  margin: 0;
}
canvas {
  display: block;
}
</style>
