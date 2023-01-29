<script>
export default{
  data() {
    return {
      search:'',
      quizes:null
    }
  },
  methods: {
    async getData(){
      const URL = 'http://localhost:3000/posts'
      const response = await fetch(URL)
      this.quizes = await response.json()
    }
  },
  mounted() {
    this.getData()
  },
  updated() {
  },
  watch:{
    search(){
      this.quizes = this.quizes.filter(item => item.body.toLowerCase().includes(this.search.toLowerCase()))
    }
  }
}
</script>

<template>  
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input type="text" v-model="search" placeholder="search...">
    </header>
    <div class="options-container">
      <div v-for="show in quizes" :key="show.id" class="card">
        <img :src="show.image" alt="no image">
        <div class="text">
          <h2>{{ show.body }}</h2>
          <p>{{ show.quantity }} questions</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container{
  max-width: 1280px;
  margin: 0 auto ;
}
header{
  margin: 30px 0 10px 0  ;
  display: flex;
  align-items: center;
}
header h1{
  font-weight: bold;
  margin-right: 30px ;
}
header input {
  padding: 6px;
  border-radius: 5px ;
  border: none ;
}
.card{
  width: 300px;
  overflow: hidden;
  border-radius: 3%;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
  margin: 0 20px 35px 0;
  cursor: pointer ;
}
.card img {
  width: 100%;
  height: 190px;
  margin: 0 ; 
}
.options-container{
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px ;
}
.text{
  background: white ;
  color: black;
}
</style>