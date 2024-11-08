<template>
  <h3 class="header">视频截屏</h3>

  <video class="video" :src="videoSrc" @play="onPlay" ref="videoPlayer" controls></video>
  <br>
  <button @click="captureFrame">捕获当前帧</button>
  <br>
  <img class="img" v-if="frameImage" :src="frameImage" mode="widthFix"></img>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const frameImage = ref<string>('');
const videoPlayer = ref<any>(null);
const videoSrc = ref('/media/test.mp4');
const name = ref('jjwu')


const onPlay = () => {

}

const captureFrame = () => {
  console.log(name.value);
  console.log(videoSrc.value)
  const player = videoPlayer.value;
  if (player) {
    const canvas = document.createElement('canvas');
    const context:any = canvas.getContext('2d');
    canvas.width = player.videoWidth;
    canvas.height = player.videoHeight;
    context.drawImage(player, 0, 0, canvas.width, canvas.height);
    const value = canvas.toDataURL('image/png');
    frameImage.value = value;
  }
}



</script>

<style scoped>
.header {
  width: 100%;
}
.video {
  width: 300px;
  height: 300px;
}
.img {
  margin-top: 20px;
  width: 300px;
  height: 300px;
}
</style>
