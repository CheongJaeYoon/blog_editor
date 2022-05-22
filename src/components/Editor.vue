<template>
<div class="editor">
  <div class="Folder"></div>
  <input class="title-editor" v-model="title">
  <div class="middle-body">
  <textarea v-model="markDownText" class="text-editor"></textarea>
  <div v-html="markedText" class="text-viewer"></div>
  </div>
  <div class="save-button"></div>
</div>
</template>
<script>
import marked from 'marked'
import { mapState } from 'vuex';
export default {
  name: 'Editor',
  data () {
    return {
      markDownText: '',
      markedText: '',
      title: '',
    }
  },
  methods: {
    img_url_to_Base64 (val, src) {
      return val.replace(src, require(`@/assets/category/${this.$store.state.currentPost}/${decodeURIComponent(src)}`))
    }
  },
  created() {
    
  },
  computed: mapState(['currentPost']),
  watch: {
    currentPost: function(val){
      this.markDownText = require(`@/assets/category/${this.$store.state.currentPost}/index.json`).content;
      this.title = this.$store.state.currentPost.split("/")[1];
      console.log(this.title)
      let temp = marked(this.markDownText);
      this.markedText = temp.replace(/<img[^>]*src=[\"']?([^>\"']+)[\"']?[^>]*>/, this.img_url_to_Base64)
    },
    markDownText: function(val){
      let temp = marked(this.markDownText);
      this.markedText = temp.replace(/<img[^>]*src=[\"']?([^>\"']+)[\"']?[^>]*>/, this.img_url_to_Base64)
    }

  }
}
</script>
<style scoped>
  .editor{
    width: 100%;
    height: 99%;
    display: flex;
    flex-direction: column;
  }
  .middle-body{
    display: flex;
    flex-direction: row;
    height: 1200px;
  }
  .text-editor{
    height: 100%;
    width: 50%;
  }
  .text-viewer{
    height: 100%;
    width: 50%;
  }
</style>