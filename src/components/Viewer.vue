<template>
  <div class="viewer">
    <div class="viewer-buttons">
      <button @click="previousPage" class="viewer-btn">Previous page</button>
      <button @click="nextPage" class="viewer-btn">Next page</button>
    </div>
    <div class="viewer-frame" v-if="getData" >
      <span v-if="getData.type === 'txt'">
        {{ getData.val }}
      </span>
      <iframe
        v-else
        :src="getData.val"
        width="100%"
        height="100%"
      />
    </div>
  </div>
</template>

<script>

export default {
  name: 'Viewer',
  props: {
    book: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      index: 0
    }
  },
  methods: {
    previousPage () {
      if (this.index > 0) this.index--
    },
    nextPage () {
      if (this.index < this.book.length - 1) this.index++
    }
  },
  computed: {
    getData () {
      if (!this.book.length) return
      return this.book[this.index]
    }
  }
}
</script>

<style scoped>
.viewer {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 2rem;
}
.viewer-buttons {
  flex-direction: column;
  margin-bottom: .5rem;
}
.viewer-frame {
  margin: 1rem auto;
  padding: 1rem;
  width: 600px;
  height: 600px;
  border: solid .05rem black;
}
iframe {
  border: none;
}
</style>
