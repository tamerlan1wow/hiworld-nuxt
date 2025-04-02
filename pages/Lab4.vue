<template><main class="flex flex-col flex-grow justify-center items-center flex-grow bg-no-repeat bg-cover bg-center" style="background-image: url('/images/Tobey.jpg'); background-size: cover;">
  
    
    <div class="flex gap-4 mb-6">
      <label class="Spider" v-for="(picture, index) in pictures" :key="index">
        <input class="mx-2" type="radio" :value="picture.name" v-model="selectedpic">
        {{ picture.name }}
      </label>
    </div>
    

    <div class="flex flex-col items-center gap-4">
      
      <div v-if="selectedImage" class="blockcap" @click="toggleAudio">
        <img :src="selectedImage" class="w-60 h-60 object-cover rounded-lg">
        <p class="text-black text-xl">{{ selectedpic }}</p>
      </div>

      <div v-if="selectedVid" class="block2">
        <video ref="videoPlayer" controls autoplay class="w-full h-[350px] object-cover rounded-lg">
          <source :src="selectedVid" type="video/mp4">
        </video>
      </div>

      <audio ref="audio" src="/audio/Title.mp3"></audio>
    </div>
  </main>

</template>

<script setup lang="ts">
import { ref, computed, reactive, watch, onMounted } from 'vue'

interface Stking {
  name: string,
  image: string
}

interface Stking2 {
  name: string,
  video: string
}

const pictures = reactive<Stking[]>([
  { name: 'Spider-man 1', image: '/images/Spiderman1.jpg' },
  { name: 'Spider-man 2', image: '/images/Spiderman2.jpg' },
  { name: 'Spider-man 3', image: '/images/Spiderman3.jpg' }
])

const videos = reactive<Stking2[]>([
  { name: 'Spider-man 1', video: '/videos/Spider1.mp4' },
  { name: 'Spider-man 2', video: '/videos/Spider2.mp4' },
  { name: 'Spider-man 3', video: '/videos/Spider3.mp4' }
])

const selectedpic = ref<string>('Spider-man 1')
const audio = ref<HTMLAudioElement | null>(null)
const videoPlayer = ref<HTMLVideoElement | null>(null)
const isPlaying = ref(false)


const selectedImage = computed(() => pictures.find(item => item.name === selectedpic.value)?.image || '')
const selectedVid = computed(() => videos.find(item => item.name === selectedpic.value)?.video || '')

const toggleAudio = () => {
  if (audio.value) {
    if (isPlaying.value) {
      audio.value.pause()
    } else {
      audio.value.play()
    }
    isPlaying.value = !isPlaying.value
  }
}


watch(selectedpic, () => {
  if (videoPlayer.value) {
    videoPlayer.value.load()
    videoPlayer.value.play()
  }
})

onMounted(() => {
  audio.value = new Audio('/audio/Title.mp3')
})
</script>

<style scoped>
.Spider {
  background-color: snow;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  padding: 8px;
  text-align: center;
}

.block2 {
  width: 100%;
  max-width: 900px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.blockcap, .Spider {
  @apply flex flex-col gap-2 border-blue-500 border bg-blue-300 w-72 h-auto items-center hover:border-red-500 hover:border-4 hover:bg-red-300 rounded-xl p-2;
}
</style>
