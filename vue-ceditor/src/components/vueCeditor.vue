<template>
  <div class="vueCeditor">
    <selectors id="selectors"></selectors>
    <textInput id="textInput" :datas.sync="inputText" v-model="inputText"></textInput>
    <textShow id="textShow" :datas.sync="innerHtml"></textShow>
  </div>
</template>

<script>
  import TextInputArea from "./TextInputArea";
  import TextShowArea from "./TextShowArea";
  import Prism from "prismjs";
  import showdown from "showdown";
  import Selectors from "./Selectors";
  import Vue from 'vue'
  Vue.use(Prism)
  let converter=new showdown.Converter();
  converter.setOption('tables',true)
  export default {
    name: "vueCeditor",
    components:{
      textInput:TextInputArea,
      textShow:TextShowArea,
      selectors:Selectors
    },
    data(){
        return{
           inputText:"",
           innerHtml:""
        }
    }
    ,
    methods:{
      makeHtml:async function (){
        this.innerHtml=converter.makeHtml(this.inputText)
        Prism.highlightAll()
      }
    },
    mounted() {
      this.innerHtml=converter.makeHtml(this.inputText)
      Prism.highlightAll()
    }
  }
</script>

<style scoped>
.vueCeditor{
  width:1300px;
  height: 800px;
  position: absolute;
  margin: 0 auto;
}
#textInput{
  width: 49%;
  height: 94%;
  position: absolute;
  left:0px;
  top:6%;
  border-radius: 20px;
}
#textShow{
  width: 49%;
  height: 94%;
  position: absolute;
  right:0px;
  top:6%;
  border-radius: 20px;
  word-wrap:break-word;
}
#selectors{
  position: absolute;
  width: 100%;
  height: 5%;
  top: 0.4%;
  left: 0px;
}
</style>
