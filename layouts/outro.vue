<template>
  <h1>{{props.title}}</h1>
  <div class="flex w-full items-center justify-center">
    <a :href="props.url">
      <qrcode :value="props.url" class="mb-2 mt-2"> </qrcode>
      <span>{{ props.url }}</span>
    </a>
  </div>
</template>
<script setup lang='ts'>
type Props = { url: string, title: string }
const props = withDefaults(defineProps<Props>(), {title: "Thanks for Listening 🙏"})
</script>
