<template>



<div v-if="article"   class="grid md:grid-cols-3 my-4  gap-4">
   <div class="md:flex flex-col"></div>
      <div class="flex flex-col shadow-md  p-2 md:p-6 text-center rounded">
        <h3 class="text-2xl text-gray-600  font-bold mb-4 text-center rounded">
           {{article.title}}
           
        </h3>
        <p>{{article.description}}</p>
         <div class="text-3xl mb-4">
            <span class="text-center"> 
              <img class="object-contain h-48 w-full" :src="article.urlToImage" alt="">
            </span>
        </div>
        <p class="text-xl mb-4">{{article.content}}</p>
       

        <div class=" my-4">
            <span class="">
                <a target="_blank" class="bg-red-600 p-3 text-white my-4 rounded hover:bg-red-500" 
                :href="article.url"
                >Read on source site</a>
             </span>
        </div>
    </div>
   </div>

   <div v-else class="grid md:grid-cols-3 my-4  gap-4">

   </div>

    <!-- <main v-if="article" class="grid md:grid-cols-3 my-4  gap-4">
        <p>{{article.content}}</p>
  <img :src="article.urlToImage" alt="">
  <a target="-blank" :href="article.url">visit on source</a>
    </main>

    <main v-else>
        News is loading...
    </main> -->

  
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
    //   console.log(this.data)
    //   console.log(this.data.data.articles[id])
    //   console.log(this.id)

      this.article = this.data.data.articles[id]

    })


} 
}
</script>

<style>

</style>