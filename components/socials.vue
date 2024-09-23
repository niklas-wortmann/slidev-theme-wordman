<script setup lang="ts">

import { ref } from 'vue'
import { useMotions } from "@vueuse/motion";
import {  computed } from 'vue'
type Socials = { twitter: string, linkedin: {name: string, path: string}, github: string, animated?: boolean, homepage: string }
const props = defineProps<Socials>()

import {onSlideEnter, useNav, useSlideContext} from '@slidev/client'


// Add a reactive index to track the current social link
const { currentSlideNo } = useNav();
const currentIndex = computed(() => {
  return (currentSlideNo.value-2) % 4
})


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
  <div v-else-if="$slidev.nav.currentPage !== 1">
      <div v-if="props.twitter && currentIndex === 0">
        <a :href="`https://twitter.com/${props.twitter}`"><mdi:twitter /> @{{props.twitter}}</a>
      </div>
      <div v-if="props.linkedin && currentIndex === 1">
        <a :href="`https://www.linkedin.com/in/${props.linkedin.path}`"><mdi:linkedin /> {{props.linkedin.name}}</a>
      </div>
      <div v-if="props.github && currentIndex === 2">
        <a :href="`https://github.com/${props.twitter}`"><mdi:github /> {{props.github}}</a>
      </div>
      <div v-if="props.homepage && currentIndex === 3">
        <a :href="`${props.homepage}`"><mdi:home-circle-outline /> {{props.homepage}}</a>
      </div>
  </div>
</template>