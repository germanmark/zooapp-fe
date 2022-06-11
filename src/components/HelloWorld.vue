<template>
  <div class="hello">
    <input 
    v-model="animalName"
    type="text" id="nameInput">
    <input 
    v-model="imageURL"
    type="text" id="imageInput">
    <button
    @click="postAnimal"
    >POST</button>
    <button
    @click="getAnimals"
    >GET</button>

    <div
    v-for="animal in animalArr"
    :key="animal.animalId"
    >
      {{animal.animalId}}
      <h1>{{animal.animalName}}</h1>
      <img :src="animal.imageURL">
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      animalName: null,
      imageURL: null,
      animalArr : []
    }
  },
  methods: {
    postAnimal() {
      axios.request({
        url : "http://127.0.0.1:5000/api/animals",
        method : "POST",
        data : {
          animalName : this.animalName,
          imageURL : this.imageURL
        }
      }).then(()=>{
        this.getAnimals();
      }).catch((error)=>{
        console.log(error);
      })
    },
    getAnimals(){
      console.log("Running GET");
      axios.request({
        url : "http://127.0.0.1:5000/api/animals",
        method : "GET"
      }).then((response)=>{
        console.log(response);
        this.animalArr = response.data;
      }).catch((error)=>{
        console.log(error);
      })
    },
    
  },
  mounted () {
      this.getAnimals();
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
