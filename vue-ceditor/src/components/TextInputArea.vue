<template>
  <div class="TextInputArea">
    <textarea @keydown="changeText()" @keyup="changeText()" v-model="inputText"></textarea>
  </div>
</template>

<script>
  import Prism from "prismjs"
  export default {
    name: "textInputArea",
    props:["datas"],
    data(){
      return{
        inputText:""
      }
    },
    methods:{
      changeText:function (e){
        this.$emit("update:datas",this.inputText)
        this.$parent.makeHtml()
      }
    },
    mounted() {
      this.inputText=this.datas
      // document.addEventListener('paste',function (event){
      //   console.log(event.clipboardData.items[0])
      //   var items = event.clipboardData && event.clipboardData.items;
      //   var file = null;
      //   if (items && items.length) {
      //     // 检索剪切板items
      //     for (var i = 0; i < items.length; i++) {
      //       console.log(items[i].type)
      //       if (items[i].type.indexOf('image') !== -1) {
      //         file = items[i].getAsFile();
      //         break;
      //       }
      //     }
      //   }
      // })
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
