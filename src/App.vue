<template>
<Header/>
<div class="container mb-10">
  <router-view/>
</div>
  <Footer/>
</template>


<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'
export default {
  name:"App",
  components:{
    Header,Footer
  }
}
</script>



<style >
</style>
