<template>
    <div class="videocam-container">
      <video ref="videoElem" autoplay></video>
      <button class="btn" @click="startStream" v-if="!isStreaming">Начать трансляцию</button>
      <button class="btn" @click="stopStream" v-if="isStreaming">Остановить трансляцию</button>
    </div>
</template>
  
<script>
export default {
    data() {
      return {
        isStreaming: false,
        stream: null,
      }
    },
    methods: {
      async startStream() {
        try {
          this.stream = await navigator.mediaDevices.getUserMedia({ video: true });
          this.$refs.videoElem.srcObject = this.stream;
          this.isStreaming = true;
        } catch (error) {
          console.error('Ошибка при запуске потока:', error);
        }
      },
      stopStream() {
        this.stream.getTracks().forEach((track) => track.stop());
        this.$refs.videoElem.srcObject = null;
        this.isStreaming = false;
      },
    },
};
</script>
  
<style>
  .videocam-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  video {
    margin-bottom: 12px;
    width: 100%;
    max-width: 400px;
    height: 400px;
    border-radius: 8px;
    background: #F6F6F6;
  }
  
  .btn {
    height: 46px;
    width: 249px;
    padding: 12px 24px;
    border-radius: 8px;
    border-color: transparent;
    background: #0000FF;
    color: #fff;
    text-align: center;
    font-size: 16px;
    font-style: normal;
    font-weight: 700;
    line-height: 18px
  }

  .btn:hover {
    opacity: 0.7;
    transition: opacity .3s ease-in-out;
  }
</style>