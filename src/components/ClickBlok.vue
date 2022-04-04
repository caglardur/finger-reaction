<template>
  <div class="block" v-if="showBlock" @click="stopTimer">click me</div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from "vue"

export default defineComponent({
  name: "ClickBlok",
  props: {
    delay: {
      require: true,
      type: Number as PropType<number>
    }
  },
  setup() {
    const showBlock = ref(false)
    const timer = ref<number | undefined>(undefined)
    const reactionTime = ref(0)
    return { showBlock, timer, reactionTime }
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true
      this.startTimer()
    }, this.delay)
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 5
      }, 5)
    },
    stopTimer() {
      clearInterval(this.timer)
      this.$emit("end", this.reactionTime)
    }
  }
})
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
