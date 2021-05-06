<template class="container">
<main class="grid md:grid-cols-3 my-4  gap-4" v-if="!data" >
  <div class="md:flex flex-col"></div>
  <div class="flex flex-col   p-2 md:p-6 text-center ">
  <h2 class="text-3xl mb-10">News Loading...</h2>
  <div class="text-2xl my-10 ">
            <span class="text-center"> 
              <img class="object-contain h-48 w-full" src="../assets/loader.gif" alt="">
            </span>
        </div>
  </div>
</main>


<main v-else class=" justify-items-center">

  <div class="">
    <div class="flex flex-col text-center">
      <p class="font-bold text-3xl text-blue-400">Select a news source</p>
<SourceSelect @set-source="setSource" :sources="source.data.sources"/>
</div>
</div>
<div class="grid grid-rows-2"></div>
<div v-for="(a,i) in data.data.articles" :key="i"  class="grid md:grid-cols-3 my-4  gap-4">
   <div class="md:flex flex-col"></div>
      <div class="flex flex-col shadow-md  p-2 md:p-6 text-center rounded">
        <h3 class="text-2xl text-gray-600  font-bold mb-4 text-center rounded">
           {{a.title}}
        </h3>
        <div v-if="a.urlToImage" class="text-2xl mb-4">
            <span class="text-center"> 
              <img class="object-contain h-48 w-full" :src="a.urlToImage" alt="">
            </span>
        </div>

        <div v-if="news_source" class="text-xl my-4">
            <span class="text-center ">
                <router-link :to="{name:'Single',params:{source:news_source,id:i}}" target="_blank" class="bg-red-500 p-3 rounded text-white hover:bg-red-300 hover:text-dark">Read More</router-link>
            </span>
        </div>
    </div>
   </div>
  


  <!-- <div  class="grid md:grid-cols-3 gap-4" v-for="(a,i) in data.data.articles" :key="i">
    <div class="flex flex-col shadow-md my-3 p-2 md:p-6 text-center rounded">
    <img :src="a.urlToImage" alt="img" class="img-fluid">
       <h5>{{a.title}}</h5>
    <template v-if="news_source">
    <router-link target="_blank" :to="{name:'Single',params:{source:news_source,id:i}}">Read More</router-link>
    </template>

    </div>

  </div> -->

<!-- Business -->

   <button class="bg-yellow-400 my-4 p-3 w-full rounded text-dark hover:bg-blue-300" v-if="business== null" @click.prevent="load_business">Latest News On Business </button>

  <div class="mt-10" v-if="business" >
   
    <!-- {{business_news.data}} -->
 
  <div v-for="(b,i) in business.data.sources" :key="i" class="grid md:grid-cols-3 my-4  gap-4">
       <div class="md:flex flex-col"></div>

      <div class="flex flex-col shadow-md  p-2 md:p-6 text-center rounded">
        <h3 class="text-2xl text-gray-600  font-bold mb-4 text-center rounded">
           {{b.name}}
        </h3>
        <p class="my-5">{{b.description}}</p>

            <div class="text-2xl mb-4" v-if="b.urlToImage">
            <span class="text-center"> 
              <img class="object-contain h-48 w-full" :src="b.urlToImage" alt="">
            </span>
        </div>
        
    </div>
   
      </div>
  </div>


 <button class="bg-blue-600 my-4 p-3 w-full rounded text-white hover:bg-blue-500" v-if="business_news == null" @click.prevent="load_tech">Latest News On Technology </button>

  <div class="mt-10" v-if="business_news" >
   
    <!-- {{business_news.data}} -->
 
  <div v-for="(b,i) in business_news.data.sources" :key="i" class="grid md:grid-cols-3 my-4  gap-4">
       <div class="md:flex flex-col"></div>

      <div class="flex flex-col shadow-md  p-2 md:p-6 text-center rounded">
        <h3 class="text-2xl text-gray-600  font-bold mb-4 text-center rounded">
           {{b.name}}
        </h3>
        <p class="my-5">{{b.description}}</p>
        
    </div>
   
      </div>
  </div>







  </main>
</template>
  <style >
      img{
        width: 300px;
        height: 300px;
      }
  </style>
<script>
import axios from 'axios'
import SourceSelect from '@/components/SourceSelect'
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
    SourceSelect,
  },
  data(){
    return{
      data:null,
      source: null,
        API_KEY :'2eefc3444c7b4ddf9a67690f8c3b121f',
        news_source: null,
        business_news: null,
        business: null

    }
  },

  methods:{
    setSource(source){
      this.data = null
      this.news_source = source
      // alert(source)
       axios.get(`https://newsapi.org/v2/top-headlines?sources=${source}&apiKey=${this.API_KEY}`)
    .then((res)=>{
      this.data = res
      console.log(this.data)
    })
    },

    load_tech(){
      // this.data = null 
      axios.get(`https://newsapi.org/v2/sources?category=technology&apiKey=${this.API_KEY}`)
      .then(res=>{
        // this.data = null 
        this.business_news = res 

        window.scroll()
        
        // console.log(this.data.data.sources.map(e=>e.name))

      })
    },

      load_business(){
      // this.data = null 
      axios.get(`https://newsapi.org/v2/sources?category=business&apiKey=${this.API_KEY}`)
      .then(res=>{
        // this.data = null 
        this.business = res 
    
        window.scroll()
        
        // console.log(this.data.data.sources.map(e=>e.name))

      })
    }


    

  },



  created(){

    const API_KEY = 'f3cb2aac48924c8c97718509ad481ee9'

//     const options = {
//   method: 'GET',
//   url: `https://newsapi.org/v2/top-headlines?country=us&apiKey=${this.API_KEY}`,
//   headers: {
//     'User-agent': 'your bot 0.1',
 
//   }
// };

    axios.get(`https://newsapi.org/v2/top-headlines?country=us&apiKey=${this.API_KEY}`)
    .then((res)=>{
      this.data = res
      // console.log(res)
    })





    axios.get('https://newsapi.org/v2/sources?apiKey=2eefc3444c7b4ddf9a67690f8c3b121f')
    .then(res=>{
      this.source = res
    })

  }
}
</script>
