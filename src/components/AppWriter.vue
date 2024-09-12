<template>
  <div>
    <VueWriter
      :array='arr'
      :typeSpeed="100"
      :eraseSpeed="40"
    />

    <br>
    <br>
    <AppBtn v-if="show" @click="$emit('next')">
      Next
    </AppBtn>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
// eslint-disable-next-line @typescript-eslint/ban-ts-comment
// @ts-ignore
import VueWriter from 'vue-writer'
import AppBtn from '@/components/AppBtn.vue'

export default defineComponent({
  name: 'AppWriter',
  components: {
    VueWriter,
    AppBtn
  },
  data () {
    return {
      show: false,
      arr: [
        'I love you a lot, Papa!',
        'And I mean it, no doubt',
        'This is how I truly feel',
        'It’s a constant, unchanging fact',
        'So many experiences...',
        'Like no one else in my life.',
        'And there’s plenty more to come.',
        'Things we can only share with each other',
        'You’ve always been there for me, and I’m here for you',
        'This kind of loyalty and support is rare. That’s how I see it.'
      ]
    }
  },
  mounted () {
    setTimeout(() => {
      this.show = true
    }, 40000)
  }
})
</script>

<style>
.is-typed {
  font-size: 1.5rem;
}

.is-typed span.typed {
  color: black;
}

.is-typed span.cursor {
  display: inline-block;
  width: 3px;
  background-color: black;
  animation: blink 1s infinite;
}

.is-typed span.underscore {
  display: inline-flex;
  width: 10px;
  height: 1px;
  align-items:flex-end;
  background-color: black;
  animation: blink 1s infinite;
}

.is-typed span.cursor.typing {
  animation: none;
}

@keyframes blink {
  49% {
    background-color: black;
  }
  50% {
    background-color: transparent;
  }
  99% {
    background-color: transparent;
  }
}
</style>
