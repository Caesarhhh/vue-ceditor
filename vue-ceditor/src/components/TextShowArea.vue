<template>
<div class="TextShowArea">
<div v-highlight class="textShow" v-html="datas"></div>
</div>
</template>

<script>
  export default {
    name: "textShowArea",
    props:["datas"],
    methods:{
    }
  }
</script>

<style scoped>
.TextShowArea{
  border-style: solid;
  border-width: thin;
}
.textShow{
  width:94%;
  height: 94%;
  position: absolute;
  top:3%;
  left:3%;
  border:none;
  outline: none;
  text-align: left;
}
</style>
