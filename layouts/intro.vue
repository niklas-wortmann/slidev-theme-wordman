<template>
  <cover>
    <div class="slidev-layout intro">
      <div class="my-auto">
        <slot />
      </div>
    </div>
  </cover>
</template>
<script setup lang="ts">
import Cover from "./cover.vue";
</script>
