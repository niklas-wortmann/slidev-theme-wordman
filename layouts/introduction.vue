<template>
  <div class="grid grid-cols-2 w-full h-full auto-rows-fr">
    <div class="w-full h-full" :style="style" />
    <div class="slidev-layout default">
      <div class='flex items-center h-full'>
        <div class="grid grid-cols-2 gap-4">
          <card title='Developer Advocate' imagePath='jbLogo.png' imageAlt='JetBrains Logo'></card>
          <card title='Core Team Member' imagePath='rxLogo.png' imageAlt='RxJS Logo'></card>
          <card title='GDE' imagePath='angularLogo.png' imageAlt='Angular Logo'></card>
          <card title='Host' imagePath='podcastLogo.png' imageAlt='Angular Plus Show Podcast Logo'></card>
        </div>
      </div>    </div>
  </div>

</template>
<script setup lang="ts">
import Card from "../components/card.vue";
import {computed, CSSProperties} from "vue";
const style = computed(() => handleBackground("headshot.png", false, "cover"))

function resolveAssetUrl(url: string) {
  if (url.startsWith('/'))
    return import.meta.env.BASE_URL + url.slice(1)
  return url
}

function handleBackground(background?: string, dim = false, backgroundSize = 'cover'): CSSProperties {
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
            ? dim
                ? `linear-gradient(#0005, #0008), url(${resolveAssetUrl(background)})`
                : `url("${resolveAssetUrl(background)}")`
            : undefined,
    backgroundRepeat: 'no-repeat',
    backgroundPosition: 'center',
    backgroundSize,
  }

  if (!style.background)
    delete style.background

  return style
}

</script>
