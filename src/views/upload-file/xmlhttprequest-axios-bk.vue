<template>
  <input type="file" @change="handleFileUpload($event)">
  <button @click="submitFile">
    Submit
  </button>
  <div>状态：<span>{{ uploadStatus }}</span></div>
</template>

<script setup lang="ts">
  type UploadStatus = 'ready' | 'loading' | 'success' | 'fail'

  const file = ref<File | null>(null)
  const uploadStatus = ref<UploadStatus>('ready')

  function handleFileUpload(event: Event) {
    const target = event.target as HTMLInputElement
    if (target.files) file.value = target.files[0]
  }
  function submitFile() {
    const formData = new FormData()
    formData.append('file', file.value as File)

    const xhr = new XMLHttpRequest()
    xhr.addEventListener('load', () => {
      uploadStatus.value = 'success'
    })
    xhr.addEventListener('error', () => {
      uploadStatus.value = 'fail'
    })
    xhr.open('POST', '/proxy/route/upload')
    uploadStatus.value = 'loading'
    xhr.send(formData)
  }
</script>
