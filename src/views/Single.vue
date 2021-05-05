<template>
  single page {{id}} source {{source}}

  <!-- {{article}} -->

  <!-- <h3>{{article.title}}</h3> -->

    <main v-if="article">
        <p>{{article.content}}</p>
  <img :src="article.urlToImage" alt="">
    </main>

    <main v-else>
        News is loading...
    </main>

  
</template>

<script>
import axios from 'axios'
export default {
name:'Single',
data(){
    return{
        data: [],
        API_KEY : '2eefc3444c7b4ddf9a67690f8c3b121f',
        id: this.$route.params.id,
        source: this.$route.params.source,
        article: null
    }
},
methods:{

},
mounted(){

     axios.get(`https://newsapi.org/v2/top-headlines?sources=${this.source}&apiKey=${this.API_KEY}`)
    .then((res)=>{
    const id = this.id
      this.data = res
      console.log(this.data)
      console.log(this.data.data.articles[id])
      console.log(this.id)

      this.article = this.data.data.articles[id]

    })


} 
}
</script>

<style>

</style>