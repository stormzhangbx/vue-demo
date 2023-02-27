<template>
  <input type="file" @change="handleFileUpload($event)">
  <button @click="submitFile">
    Submit
  </button>
</template>

<script setup lang="ts">
  import api from '@/api/index'

  const file = ref<File | null>(null)

  function handleFileUpload(event: Event) {
    const target = event.target as HTMLInputElement
    if (target.files) file.value = target.files[0]
  }
  async function submitFile() {
    const formData = new FormData()
    formData.append('file', file.value as File)

    await api.post('/route/upload', formData)
  }
</script>
