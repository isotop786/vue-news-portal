<template>
<main v-if="!data">
  Loading news....
</main>


<main v-else>
<SourceSelect @set-source="setSource" :sources="source.data.sources"/>
  <!-- {{data.data.articles[3].title}} -->
  <!-- {{source.data.sources[3].id}} -->
  <!-- <select >
    <option value="0">select source</option>
    <option v-for="s in source.data.sources" :key="s.id"  :value="s.id">{{s.id}}</option>
  </select> -->
  <div v-for="(a,i) in data.data.articles" :key="i">
    <p>{{a.title}}</p>
    <img :src="a.urlToImage" alt="img" >
    <template v-if="news_source">
    <router-link target="_blank" :to="{name:'Single',params:{source:news_source,id:i}}">Read More</router-link>
    </template>
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
        news_source: null

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
    }
  },



  created(){

    const API_KEY = '2eefc3444c7b4ddf9a67690f8c3b121f'

    axios.get(`https://newsapi.org/v2/top-headlines?country=us&apiKey=${this.API_KEY}`)
    .then((res)=>{
      this.data = res
      console.log(this.data)
    })


    axios.get('https://newsapi.org/v2/sources?apiKey=2eefc3444c7b4ddf9a67690f8c3b121f')
    .then(res=>{
      this.source = res
    })

  }
}
</script>
