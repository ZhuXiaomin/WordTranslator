<template>
  <div class="row" id="translateForm">
      <div class="col-md-6 col-md-offset-3">
        <form id="transForm" class="well form-inline" @submit="formSubmit">
          <input class="form-control" type="text" v-model="textToTranslate" placeholder="Enter words ...">
          <select class="form-control" v-model="language">
            <option value="ru">Russian</option>
            <option value="es">Spanish</option>
            <option value="fr">French</option>
            <option value="zh">Chinese</option>
          </select>
          <input class="btn btn-primary" type="Submit" name="" value="Translate">
        </form>
      </div>
  </div>
</template>

<script>
export default {
  name: 'translateForm',
  data(){
    return {
      textToTranslate: '',
      language:''
    }
  },
  created(){
    this.language = 'ru';
  },
  methods:{
    formSubmit (e) {
        // alert(this.textToTranslate);
        this.textToTranslate = this.textToTranslate.replace(/\s+/g, "");
        if(this.textToTranslate == ""){
          console.log('Text is empty!');
          return false;
        }
        this.$emit('formSubmit', this.textToTranslate, this.language);
        e.preventDefault();
    }
  }
}
</script>

<style>
#transFrom{
  border-radius: 10px;
  border: 1px #ccc solid;
}
</style>
