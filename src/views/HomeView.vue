<template>
  <div class="home">
    <h1 v-if="step === 0" class="text-big animate__animated animate__backInDown">
      Hello Papa!!
    </h1>
    <h1 v-if="step === 1" class="text-regular animate__animated animate__fadeIn">
      It’s a great day, isn’t it?
    </h1>
    <h1 v-if="step === 2" class="text-regular animate__animated animate__pulse">
      It’s your birthday 🙂
    </h1>
    <div v-if="step === 3">
      <h1 class="text-regular animate__animated animate__pulse animate__infinite">
        The main person today is you, <b>Dad</b>
      </h1>
      <div class="text-regular animate__animated animate__headShake animate__infinite">
        💪💪💪
      </div>
    </div>

    <h1 v-if="step === 4 || step === 5 || step === 6" class="text-regular animate__animated animate__bounce" style="min-height: 400px;">
      This gift was made just for you 🎁

      <div v-if="step === 5 || step === 6" class="text-small animate__animated animate__fadeIn" style="margin-top: 30px;">
        From your son, Akash.
      </div>

      <div v-if="step === 6" class="text-small animate__animated animate__fadeIn" style="margin-top: 30px;">
        I created it from scratch.
      </div>
    </h1>

    <div v-if="step === 7">
      <h1 class="error" style="color: white;">
        Oops. Site error(Nvm).
      </h1>
    </div>

    <h1 v-if="step === 8" class="text-regular" style="display: flex">
      <div class="animate__animated animate__swing animate__infinite">😂</div>
      I can’t resist a joke(Here we go again)
      <div class="animate__animated animate__swing animate__infinite">😂</div>
    </h1>

    <h1 v-if="step === 9" class="text-regular animate__animated animate__zoomIn">
      Let’s get to the main part.
      <br>
      <br>

      <AppBtn class="animate__animated animate__bounce animate__delay-1s" @click="step++">
        Let’s go
      </AppBtn>
    </h1>

    <AppWriter v-if="step === 10" @next="onWriterNext" />

    <AppAvatarScreen v-if="step === 11" />

    <audio
      :src="require('@/assets/music.mp3')"
      ref="music"
      preload
      loop
    ></audio>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import anime from 'animejs'
import 'animate.css'
import AppBtn from '@/components/AppBtn.vue'
import AppWriter from '@/components/AppWriter.vue'
import AppAvatarScreen from '@/components/AppAvatarScreen.vue'

export default defineComponent({
  name: 'HomeView',
  data (): {
    [key: string]: any
    } {
    return {
      step: 0,
      text: 'Hello',
      interval: null
    }
  },
  components: {
    AppBtn,
    AppWriter,
    AppAvatarScreen
  },
  methods: {
    onWriterNext () {
      this.step++

      setTimeout(() => {
        (this.$refs.music as HTMLAudioElement).play()
      }, 2000)
    }
  },
  watch: {
    step (step) {
      if (step === 7) {
        clearInterval(this.interval)

        document.body.style.background = 'red'

        setTimeout(() => {
          document.querySelector('.error')!.className += ' animate__animated animate__hinge'

          setTimeout(() => {
            this.step++

            document.body.style.background = 'initial'

            setTimeout(() => this.step++, 3000)
          }, 2000)
        }, 3000)
      }
    }
  },
  mounted () {
    document.addEventListener('keydown', (e) => {
      this.step = parseInt(e.key)
      clearInterval(this.interval)
    })

    this.interval = setInterval(() => this.step++, 3000)
  },
  unmounted () {
    clearInterval(this.interval)
  }
})
</script>

<style lang="sass">
body
  transition: all ease

.home
  height: 100%
  display: flex
  align-items: center
  justify-content: center
  text-align: center

  .text-big
    font-size: 4rem

  .text-regular
    font-size: 2rem

  .text-small
    font-size: 1.5rem

  .center
    margin: 0 auto
</style>
