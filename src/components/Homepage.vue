<template>
  <div class="homepage">
    <button @click="openModal">Add page</button>
    <modal v-if="showModal">
      <h2 slot="header">Enter a text or URL</h2>
      <div slot="body">
        <form @submit.prevent="addPage" class="homepage-form">
          <textarea v-model="contentText" placeholder="Enter text here:" class="homepage-text" />
          <input type="text" v-model="contentUrl" placeholder="Enter URL URL here:" class="homepage-url" />
          <button class='btn teal'>Add page</button>
        </form>
      </div>
    </modal>
    <viewer v-if="store.length" :book="store" />
  </div>
</template>

<script>

import Modal from '@/components/Modal'
import Viewer from '@/components/Viewer'

export default {
  name: 'Homepage',
  components: {
    Modal,
    Viewer
  },
  data () {
    return {
      showModal: false,
      showViewer: false,
      contentText: null,
      contentUrl: null,
      store: []
    }
  },
  methods: {
    openModal () {
      this.showModal = true
    },
    addPage () {
      if (!this.contentUrl && !this.contentText) alert('Vous devez renseigner un champs')

      const local = localStorage.getItem('techex')
      if (local) this.store = JSON.parse(local)

      this.store.push({
        type: this.contentText ? 'txt' : 'url',
        val: this.contentText ? this.contentText : this.contentUrl
      })

      localStorage.setItem('techex', JSON.stringify(this.store))

      this.showModal = false
      this.contentText = null
      this.contentUrl = null
    }
  }
}
</script>

<style scoped>
.homepage-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.homepage-text {
  margin: 1rem auto;
  padding: 0 10px;
  width: 500px;
  height: 100px;
}
.homepage-url {
  margin: 1rem auto;
  width: 500px;
  height: 30px;
  padding: 0 10px;
}
</style>
