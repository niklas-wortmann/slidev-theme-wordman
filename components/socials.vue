<script setup lang="ts">

type Socials = { twitter?: string, linkedin?: {name: string, path: string}, github?: string }
  const props = defineProps<Socials>()

</script>
<template>
  <div class="flex items-center justify-between" v-if="!animated">
    <div v-if="props.twitter">
      <a :href="`https://twitter.com/${props.twitter}`"><mdi:twitter /> @{{props.twitter}}</a>
    </div>
    <div v-if="props.linkedin">
      <a :href="`https://www.linkedin.com/in/${props.linkedin.path}`"><mdi:linkedin /> {{props.linkedin.name}}</a>
    </div>
    <div v-if="props.github">
      <a :href="`https://github.com/${props.twitter}`"><mdi:github /> {{props.github}}</a>
    </div>
  </div>
</template>