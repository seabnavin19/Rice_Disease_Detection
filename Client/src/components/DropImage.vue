<template>

    <div class="row">    
   <div class="card col-3 m-5" 
   :class="getClasses" 
    @dragover.prevent="dragOver" 
    @dragleave.prevent="dragLeave"
    @drop.prevent="drop($event)"
   style="width: 18rem;"> 
        <img src="../assets/drop.png" v-if="!imageSource" alt="">
       <img :src="imageSource" v-if="imageSource" class="card-img-top" />
  <div class="card-body"
    >

      
      <h1 v-if="wrongFile">Wrong file type</h1>
      <h5 class="card-title text-success">Drop an image</h5>

  </div>
   </div>

  <div class="card m-5">
  <div class="card-header">
    <h4 >{{disease}}</h4>
  </div>
  <div class="card-body">
    <h5 class="card-title">Probability: {{probability}}%</h5>
    <p class="card-text">See how we can prevent and fix it..</p>
    <a href="#" class="btn btn-success">See Details</a>
  </div>
</div>
    </div>

</template>



<script>
import axios from 'axios'

export default {
  name: 'DropAnImage',
  data(){
    return{
      isDragging:false,
      wrongFile:false,
      imageSource:null,
      result:null,
      disease:"Unknown Disease",
      probability:"0",
      diseases:["Bacterial","Brown Spot","Leaf smut"],

    }
  },
  computed:{
    getClasses(){
      return {isDragging: this.isDragging}
    }
  },
  methods:{
    dragOver(){
      this.isDragging = true
    },
    dragLeave(){
      this.isDragging = false
    },
    drop(e){
      let files = e.dataTransfer.files
      this.wrongFile = false
      // allows only 1 file
      if (files.length === 1) {
        let file = files[0]
        // allows image only
        if (file.type.indexOf('image/') >= 0) {
          var reader = new FileReader()
          reader.onload = f => {
            this.imageSource = f.target.result

            // post to api
            
        axios.post('http://localhost:5000', {"image_data":this.imageSource}, {
                }).then(res => {
                    console.log(res.data);
                    this.result= res.data[0]
                    this.disease=this.diseases[parseInt(this.result["class"])]
                    this.probability=this.result["class_probability"]
                    // this
                }).catch(err => {
                    console.log(err.response);
                });

            this.isDragging = false
          }
          reader.readAsDataURL(file)
        }else{
          this.wrongFile = true
          this.imageSource = null
          this.isDragging = false
        }
      }
    },
    onRequestUploadFiles(){
      
    }
  }
}
</script>



<style scoped>
.drop{
  width: 100%;
  height: 100%;
  background-color: #eee;
  border:10px solid #eee;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  transition: background-color .2s ease-in-out;
  font-family: sans-serif;
}
.isDragging{
  background-color: #999;
  border-color: #fff;
}
img{
  width: 100%;
  height: 100%;
  object-fit: contain;
}
</style>