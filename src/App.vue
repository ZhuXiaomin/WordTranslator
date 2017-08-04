<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <h5 class="text-muted">Powered by Vue.js</h5>
    <br>
    <TranslateForm @formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text='translatedText'></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
export default {
  name: 'app',
  components:{
    TranslateForm,
    TranslateOutput
  },
  data(){
    return {
      translatedText: ''
    }
  },
  methods:{
    translateText(text, language){
      // alert(text);
      if( text != ""){
        this.translatedText = 'Translating...';
      }
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170729T051737Z.c3f1fa0c12da73f2.ec4e03cb11d2406d3b3a56b28d83162062bdabae&text=' + text +'&lang=' + language).then(
        response => {
          console.log(response.body.text[0]);
          this.translatedText =  response.body.text[0]
        }
      )
    }
  }
}
</script>

<style lang="less">
@bg-color: #fefefe;

body{
  background-color: @bg-color;
}
</style>
