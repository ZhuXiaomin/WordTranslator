<template>
<div class="row" id="translateForm">
  <div class="col-md-6 col-md-offset-3">
    <form id="transForm" class="well form-inline" @submit="formSubmit">
      <input class="form-control" type="text" v-model="textToTranslate" placeholder="Enter words ...">
      <select class="form-control" v-model="language">
              <option v-for="option in languageOptions" :value="option.value">{{option.text }}</option>
        </select>
      <input class="btn btn-primary" type="Submit" name="" value="Translate">
    </form>
  </div>
</div>
</template>

<script>
export default {
  name: 'translateForm',
  data() {
    return {
      textToTranslate: '',
      language: '',
      languageOptions: [{
        text: 'Russian',
        value: 'ru'
      }]
    }
  },
  created() {
    this.language = 'ru';
    this.getlanguageOptions()
  },
  methods: {
    formSubmit(e) {
      // alert(this.textToTranslate);
      this.textToTranslate = this.textToTranslate.replace(/\s+/g, "");
      if (this.textToTranslate == "") {
        console.log('Text is empty!');
        return false;
      }
      this.$emit('formSubmit', this.textToTranslate, this.language);
      e.preventDefault();
    },
    getlanguageOptions() {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/getLangs?ui=zh&key=trnsl.1.1.20170729T051737Z.c3f1fa0c12da73f2.ec4e03cb11d2406d3b3a56b28d83162062bdabae').then(
        response => {
          var langs = JSON.parse(response.bodyText)['langs'];
          var tmp = new Array();
          Object.entries(langs).forEach(function(item) {
            tmp.push({
              value: item[0],
              text: item[1]
            });
          });
          this.languageOptions = tmp;
        }
      );
    }
  }
}
</script>

<style>
#transFrom {
  border-radius: 10px;
  border: 1px #ccc solid;
}
</style>
