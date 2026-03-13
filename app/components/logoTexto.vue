<script setup lang="ts">
defineProps({
  titulo: {
    type: String,
    required: true
  },
  descricao: {
    type: String,
    required: true
  },
  fota: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="flex items-center gap-2">
    <NuxtImg
      :src="fota"
      alt="Logo"
      class="w-20"
    />
    <div>
      <h1 class="text-xl font-bold">
        {{ titulo }}
      </h1>
      <p class="text-xs">
        {{ descricao }}
      </p>
    </div>
  </div>
</template>
