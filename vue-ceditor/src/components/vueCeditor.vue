<template>
  <div class="vueCeditor">
    <textInput id="textInput" :datas.sync="inputText" v-model="inputText"></textInput>
    <textShow id="textShow" :datas="innerHtml"></textShow>
  </div>
</template>

<script>
  import TextInputArea from "./TextInputArea";
  import TextShowArea from "./TextShowArea";
  import showdown from "showdown";
  let converter=new showdown.Converter();
  converter.setOption('tables',true)
  export default {
    name: "vueCeditor",
    components:{
      textInput:TextInputArea,
      textShow:TextShowArea
    },
    data(){
        return{
           inputText:"5555555555555",
           innerHtml:""
        }
    }
    ,
    methods:{
      makeHtml:function (){
        this.innerHtml=converter.makeHtml(this.inputText)
      }
    },
    mounted() {
      this.innerHtml=converter.makeHtml(this.inputText)
    }
  }
</script>

<style scoped>
.vueCeditor{
  width:1300px;
  height: 720px;
  position: absolute;
  margin: 0 auto;
}
#textInput{
  width: 49%;
  height: 100%;
  position: absolute;
  left:0px;
  top:0px;
  border-radius: 20px;
}
#textShow{
  width: 49%;
  height: 100%;
  position: absolute;
  right:0px;
  top:0px;
  border-radius: 20px;
}
</style>
