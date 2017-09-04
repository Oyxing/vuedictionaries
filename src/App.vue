<template>
  <div id="app">
  <h1>在线翻译</h1>
  <b>简单 易用  方便</b>
    <translateFrom v-on:formSubmit="translateText"></translateFrom>
    <translateOutput v-text="translateTexts"></translateOutput>
  </div>
</template>

<script>
import TranslateFrom from '@/components/TranslateFrom'
import TranslateOutput from '@/components/TranslateOutput'
export default {
  name: 'app',
  data () {
    return {
      translateTexts: ''
    }
  },
  components: {
    translateFrom: TranslateFrom,
    translateOutput: TranslateOutput
  },
  methods: {
    translateText: function (text, lang) {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170904T082057Z.316b4385d580af22.e3290fa5dd3fe2b087393bea97cebed5fc42a184&lang=' + lang + '&text=' + text)
      .then((res) => {
        console.log(res.body.text)
        this.translateTexts = res.body.text[0]
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
