<template>
<div class="Selectors">
  <div id="selectBox">
    <div class="button" @click="openPicwin">
      <img src="http://caesar216.usa3v.net/caelog/images/picture.png" alt="error">
    </div>
    <div id="ImgBox" v-if="ifwin">
      <div id="close" @click="closePicwin">
        <img :src="closeImgSrc" alt="error">
      </div>
      <div id="copy" @click="copyPic">
        复制选取的图片
      </div>
      <div id="ImgSelectArea">
        <GeminiScrollbar>
          <div v-for="(value,index) in imgs" :class="{imgSelects:index!=selectedIndex,imgSelected:index==selectedIndex}" @dblclick="copyPic()" @click="selectPic(index)">
            <img :src="value" alt="error">
          </div>
        </GeminiScrollbar>
      </div>
      <div id="upload">点击或拖拽上传本地图片</div>
    </div>
  </div>
</div>
</template>

<script>
  import Vue from 'vue'
  import axios from 'axios'
  import GeminiScrollbar from 'vue-gemini-scrollbar';
  import VueClipboard from 'vue-clipboard2'
  Vue.use(VueClipboard)
  Vue.use(GeminiScrollbar)
  export default {
    name: "Selectors",
    data(){
      return{
        imgs:[
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png",
          "http://caesar216.usa3v.net/caelog/images/picture.png"
        ],
        closeImgSrc:"http://caesar216.usa3v.net/caelog/images/close2.png",
        ifwin:false,
        selectedIndex:9999
      }
    },
    methods:{
      openPicwin:function (){
        this.ifwin=true
        this.$nextTick(()=>{
          let upload=document.getElementById("ImgSelectArea")
          upload.addEventListener('dragenter',this.onDrag,false)
          upload.addEventListener('dragover',this.onDrag,false)
          upload.addEventListener('drop',this.onDrop,false)
        })
      },
      closePicwin:function (){
        this.ifwin=false
        this.selectedIndex=9999
      },
      selectPic:function (index){
        this.selectedIndex=index
      },
      copyPic:function (){
        let text="<img src=\""+this.imgs[this.selectedIndex]+"\" width=\"200px\" />"
        this.$copyText(text)
        this.closePicwin()
      },
      onDrag (e) {
        e.stopPropagation();
        e.preventDefault();
      },
      onDrop (e) {
        e.stopPropagation();
        e.preventDefault();
        this.imgPreview(e.dataTransfer.files);
        this.uploadFile(e.dataTransfer.files)
      },
      //图片预览
      imgPreview (files) {
        let read = new FileReader();
        var that=this
        let imgUrl = document.querySelector('#preview-img');
        read.readAsDataURL(files[0]);
        read.onload = function () {
          let url = read.result;
          let img = new Image();
          img.src = url;
          console.log(url)
          that.imgs.push(url)
        }
      },
      uploadFile (files) {
        let params = new FormData();
        params.append('file', files[0]);
        axios.post('https://caelog.top:8443/uploadtemp', params).then(res=>{
          console.log(res)
        })
      }
    },
    mounted() {
    }
  }
</script>

<style scoped>
.Selectors{
}
#selectBox{
  width:98%;
  height: 100%;
  position: absolute;
  left:1%;
  top:0;
}
.button{
  width:3%;
  height: 90%;
  border-radius: 50%;
  float:left;
  margin-left: 3%;
  cursor: pointer;
}
.button img{
  width: 100%;
  height: 100%;
}
#ImgBox{
  width:50%;
  height: 1000%;
  border-style: solid;
  position: absolute;
  z-index: 2;
  background-color: white;
  border-radius: 20%;
}
#close{
  border-style: solid;
  width:5%;
  height: 8%;
  border-radius: 50%;
  position: absolute;
  right:5%;
  cursor: pointer;
  background-color: white;
  overflow: hidden;
}
#close img{
  width: 100%;
  height: 100%;
}
#copy{
  position: absolute;
  width:40%;
  height: 10%;
  left:30%;
  top:1.2%;
  font-family: 华光楷体_CNKI;
  line-height: 180%;
  font-size: 150%;
  cursor: pointer;
}
#ImgSelectArea{
  border-style: solid;
  border-radius: 10%;
  width:96%;
  height: 70%;
  position: absolute;
  left:1.8%;
  top:13%;
}
.imgSelects{
  width: auto;
  max-width: 21%;
  height: 45%;
  float: left;
  margin-left: 2%;
  margin-top: 2%;
  cursor: pointer;
  border-style: solid;
  border-radius: 30%;
  border-width: 1px;
  border-color: transparent;
}
.imgSelected{
   width: auto;
   max-width: 21%;
   height: 45%;
   float: left;
   margin-left: 2%;
   margin-top: 2%;
   cursor: pointer;
   border-style: solid;
  border-radius: 30%;
  border-width: 1px;
  border-color: lightskyblue;
 }
.imgSelects img{
  height: 100%;
}
.imgSelected img{
  height: 100%;
}
#upload{
  position: absolute;
  bottom:4%;
  font-family: 华光楷体_CNKI;
  font-size: 180%;
  left:25%;
  cursor: pointer;
}
</style>
