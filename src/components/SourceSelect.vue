<template>
   
  <select class="form-select w-full block p-3 my-2 md:my-10 border rounded" @change="onchange" v-model="selected">
      <option value="0">Select Source</option>
      <option v-for="source in sources" :key="source.id" :value="source.id">
          {{source.id}}
      </option>
  </select>
</template>

<script>
export default {
    name:"SourceSelect",
    props:['sources'],
    data(){
        return{
            selected: null
        }
    },

    methods:{
        onchange(){
        //  const source = this.sources.find((s)=>s === this.selected.id)
        // const source = this.sources.find((s)=> s.id === this.selected.id)

         console.log(this.selected)

        //  console.log(source)

        this.$emit('set-source',this.selected)
        }
    },


    created(){
        console.log("sources are"+ this.sources)
    }

}
</script>

<style>

</style>