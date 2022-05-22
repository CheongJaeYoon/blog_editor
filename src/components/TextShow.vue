<template>
<div v-html="text" class="text-show">
</div>
</template>
<script>
import marked from 'marked'
import { mapState } from 'vuex';
export default {
  name: 'TextShow',
  data () {
    return {
      text: '# abcdefg'
    }
  },
  data () {
    return {
      text: ''
    }
  },
  methods: {
    img_url_to_Base64 (val, src) {
      return val.replace(src, require(`@/assets/category/etc/뭔가 쓸데없이 긴 제목/${decodeURIComponent(src)}`))
    }
  },
  created() {
    
  },
  computed: mapState(['currentPost']),
  watch: {
    currentPost: function(val){
      let a = require(`@/assets/category/${this.$store.state.currentPost}/index.json`)
      let b = marked(a.content)
      this.text = b.replace(/<img[^>]*src=[\"']?([^>\"']+)[\"']?[^>]*>/, this.img_url_to_Base64)
      console.log(this.text)
    }

  }
}
</script>
<style scoped>
  .text-show{
    height: 100%;
    width: 100%;
    background-color: blue;
  }
</style>