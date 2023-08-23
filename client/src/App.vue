<script setup>
import NetworkCommunication from './components/NetworkCommunication.vue'
import DBtest from './components/DbNotes.vue'
import webWorker from './services/WebWorkers.js'

import { ref } from 'vue'

const _message = ref('')

function testWebWorker() {
  _message.value = 'Waiting reply...'
  webWorker.request('test').then(data => {
    _message.value = data
  }, () => {
    _message.value = 'Connection to Web Worker failed.'
  })
}
</script>

<template>
  <div class="padded">
    <h1>Web Workers</h1>
    <hr>

    <h2>Simple Web Worker test</h2>
    <p>Send the request to the Web Worker, and it will answer is 3 seconds.</p>
    <div class="flex-container padded">
      <button @click="testWebWorker()">
        Send request
      </button>
      <div class="padded">
        {{ _message }}
      </div>
    </div>

    <h2>IndexedDB access through the worker</h2>
    <DBtest />

    <h2>Network connections through the worker</h2>
    <NetworkCommunication />
  </div>
</template>

<style scoped></style>