<template>
  <div class="file_upload">
    <h3>Поле для загрузки файлов</h3>
      <form @submit.prevent="onUpload">
        <input type="file" @change="uploadFile" name="images">
        <button @click="submitFile"> Отправить</button>
      </form>
  </div>
</template>

<script>
// function getBase64Image(img) {
//   var canvas = document.createElement("canvas");
//   canvas.width = img.width;
//   canvas.height = img.height;
//   var ctx = canvas.getContext("2d");
//   ctx.drawImage(img, 0, 0);
//   var dataURL = canvas.toDataURL("image/png");
//   return dataURL.replace(/^data:image\/(png|jpg);base64,/, "");
// }


import axios from 'axios'

export default {
  name: 'FileUpload',
  data(){
    return{
      images: null
    }
  },
  props: {
    msg: String
  },methods:{
    uploadFile(event){
      alert("файлы были успешно загружены!")
      this.images = event.target.files[0];
    },
    submitFile(){
      const formData = new FormData();
      formData.append('images', this.images, this.images.name);
      axios({
        method: "POST",
        url: 'http://localhost:3081/files/file-upload',
        headers:{
          'Content-Type': 'multipart/form-data'
        },
        data: formData
      }).then((res) =>{
        console.log(res.data.files)
        console.log(res.status)
      })
    }
  }
}
</script>

