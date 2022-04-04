<template>
  <p>Reaction time: {{ score }} ms</p>
  <p class="rank">{{ rank }}</p>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from "vue"

export default defineComponent({
  name: "ResultBlok",
  props: {
    score: {
      require: true,
      type: Number as PropType<number>
    }
  },
  setup() {
    const rank = ref<string | null>(null)
    return { rank }
  },
  mounted() {
    if (this.score) {
      if (this.score < 250) {
        this.rank = "perfect"
      } else if (this.score < 400) {
        this.rank = "ehh"
      } else {
        this.rank = "poor"
      }
    }
  }
})
</script>

<style>
.rank {
  font-size: 1.4em;
  color: #0faf89;
  font-weight: bold;
}
</style>
