<template>
  <div id="translateFroms">
      <input type="text" v-model="textToTranslate" placeholder='输入翻译的内容'>
      <select v-model="language" >
        <option v-for="item in languags" :value="item.lang">{{item.title}}</option>
      </select>
      <input type="submit" v-on:click="formSubmit" value="翻译" >
  </div>
</template>

<script>
export default {
  name: 'translateFroms',
  data () {
    return {
      languags: '',
      language: '',
      textToTranslate: ''
    }
  },
  created () {
    this.Getlang()
  },
  methods: {
    formSubmit: function () {
      this.$emit('formSubmit', this.textToTranslate, this.language)
      alert(this.textToTranslate)
    },
    Getlang () {
      this.$http.get('/static/json/lang.json')
      .then((res) => {
        console.log(res.body)
        this.languags = res.body
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>

<style>

</style>
