<script setup lang="ts">

import { ref } from 'vue'
import { useMotions } from "@vueuse/motion";

type Socials = { twitter: string, linkedin: {name: string, path: string}, github: string, animated?: boolean, animationTime?: number, homepage: string }
const props = defineProps<Socials>()

const initial = {y:  100, opacity: 0};
const enter = {y: 0, opacity: 1 };
const timer = ref(0);
setInterval(x => {
  if(timer.value >= 3) {
    timer.value = 0
  } else {
    timer.value++
  }
}, props.animationTime ?? 30000)


</script>
<template>
  <div class="flex items-center justify-between" v-if="!props.animated">
    <div v-if="props.twitter">
      <a :href="`https://twitter.com/${props.twitter}`"><mdi:twitter /> @{{props.twitter}}</a>
    </div>
    <div v-if="props.linkedin">
      <a :href="`https://www.linkedin.com/in/${props.linkedin.path}`"><mdi:linkedin /> {{props.linkedin.name}}</a>
    </div>
    <div v-if="props.github">
      <a :href="`https://github.com/${props.twitter}`"><mdi:github /> {{props.github}}</a>
    </div>
    <div v-if="props.homepage">
      <a :href="`${props.homepage}`"><mdi:home-circle-outline /> {{props.homepage}}</a>
    </div>
  </div>
  <div v-else>
      <div v-if="props.twitter && timer === 0" v-motion :initial="initial" :enter="enter">
        <a :href="`https://twitter.com/${props.twitter}`"><mdi:twitter /> @{{props.twitter}}</a>
      </div>
      <div v-if="props.linkedin && timer === 1" v-motion :initial="initial" :enter="enter">
        <a :href="`https://www.linkedin.com/in/${props.linkedin.path}`"><mdi:linkedin /> {{props.linkedin.name}}</a>
      </div>
      <div v-if="props.github && timer === 2" v-motion :initial="initial" :enter="enter">
        <a :href="`https://github.com/${props.twitter}`"><mdi:github /> {{props.github}}</a>
      </div>
      <div v-if="props.homepage && timer === 3" v-motion :initial="initial" :enter="enter">
        <a :href="`${props.homepage}`"><mdi:home-circle-outline /> {{props.homepage}}</a>
      </div>
  </div>
</template>