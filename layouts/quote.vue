<template>
  <div class="grid grid-cols-2 w-full h-full auto-rows-fr">
    <div class="w-full h-full" :style="style" />
    <div class="slidev-layout default text-center" :class="props.class">
      <div class="flex" style="height: 90%">
        <span class="self-start text-8xl" style="color: var(--slidev-theme-primary)">"</span>
        <h1 class="self-center">{{props.quote}}</h1>
        <span class="self-end text-8xl">"</span>
      </div>
      <span>{{props.author}}</span>
    </div>
  </div>
</template>
<style scoped>
</style>
<script setup lang="ts">
import { computed } from 'vue'
import type { CSSProperties } from 'vue'

const props = defineProps({
  image: {
    type: String,
  },
  author: {
    type: String,
  },
  quote: {
    type: String,
  },
  class: {
    type: String,
  },
  backgroundSize: {
    type: String,
    default: 'cover',
  },
})

const style = computed(() => handleBackground(props.image, true, props.backgroundSize))

function resolveAssetUrl(url: string) {
  if (url.startsWith('/'))
    return import.meta.env.BASE_URL + url.slice(1)
  return url
}

function handleBackground(background?: string, fade = false, backgroundSize = 'cover'): CSSProperties {
  const isColor = background && (background[0] === '#' || background.startsWith('rgb'))

  const style = {
    background: isColor
        ? background
        : undefined,
    color: (background && !isColor)
        ? 'white'
        : undefined,
    backgroundImage: isColor
        ? undefined
        : background
            ? fade
                ? `linear-gradient(to right, rgba(255,153,153,0) 0%,rgba(255,153,153,0) 75%, var(--slidev-theme-background) 100%),  url(${resolveAssetUrl(background)})`
                : `url("${resolveAssetUrl(background)}")`
            : undefined,
    backgroundRepeat: 'no-repeat',
    backgroundPosition: 'center',
    "background-color": 'var(--slidev-theme-background)',
    backgroundSize,
  }

  if (!style.background)
    delete style.background

  return style
}
</script>