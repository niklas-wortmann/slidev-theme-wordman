<script setup lang="ts">
  import QrcodeVue from 'qrcode.vue'
  type PROPS  = { value: string, size?: number, margin?: number };
  const props = defineProps<PROPS>();
</script>

<template>
  <qrcode-vue :value="props.value" :size="props.size ?? 300" render-as="svg" level="M" :margin="props.margin ?? 1 "/>
</template>
