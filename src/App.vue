<template>
  <div id="app">
    <CameraStream />
  </div>
</template>

<script>
import CameraStream from './components/CameraStream.vue';

export default {
  name: 'App',
  components: {
    CameraStream,
  },
};
</script>

<style>
#app {
  margin: auto;
  max-width: 600px;
}
</style>