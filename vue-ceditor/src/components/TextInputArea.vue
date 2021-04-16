<template>
  <div class="TextInputArea">
    <textarea @keyup="changeText" v-model="inputText"></textarea>
  </div>
</template>

<script>
  export default {
    name: "textInputArea",
    props:["datas"],
    data(){
      return{
        inputText:""
      }
    },
    methods:{
      changeText:function (){
        this.$emit("update:datas",this.inputText)
        console.log(this.datas)
        this.$parent.makeHtml()
      }
    },
    mounted() {
      this.inputText=this.datas
    }
  }
</script>

<style scoped>
.TextInputArea{
  border-style: solid;
  border-width: thin;
}
textarea{
  width:94%;
  height: 94%;
  position: absolute;
  top:3%;
  left:3%;
  font-size: 20px;
  font-family: 华光楷体_CNKI;
  border:none;
  outline: none;
}
textarea:focus{
  border-width: 2px;
}
</style>
