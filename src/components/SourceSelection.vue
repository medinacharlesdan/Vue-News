<template>
  <div class="SourceSelection">
   

   <h2 class="ui header">
    <i class=" ui icon newspaper" aria-hidden="true"></i>
    <div class="content">
      Get Updated 
    </div>
    <div class="sub header">
      Select News source powered by: <a href="https://newsapi.org/docs" target="_blank"> newsapi.org</a>
    </div>
  </h2>




        <form class="ui fluid form ">
        <div class="field">
          
          <select class="ui fluid dropdown" v-on:change="sourceChanged">
          <option v-bind:value="source.id" v-for="source in sources">
            {{source.name}}
          </option>
         
          </select>

        </div>
        </form>


        <p v-if="source" class="p-top-1">
         {{source.description}}
        </p>

     

      <div class="sub header" v-show="source">
      <h3 class=""> Check out their official website</h3>
      <a :href="source.url" target="_blank">
        <button class="ui violet button right labeled icon">
           <i class="right arrow icon"></i>
          Visit {{source.name}}'s Website </button>
        </a>
      </div>


    </div>





</template>

<script>
export default {
  name: 'SourceSelection',
  data () {
    return {
      sources: [],
      source:"",
    }
  },
  created: function(){
      this.$http.get("https://newsapi.org/v2/sources?language=en&apiKey=e56ad3527e184b7c82638f3a7b47c92b").then(response => {
        this.sources = response.data.sources;
      })

      
  },
  mounted: function(){
  $('.ui.dropdown')
  .dropdown()
  ;
  },
  methods:{
    sourceChanged: function(e){
      for (let i=0; i < this.sources.length; i++){
        if (this.sources[i].id == e.target.value){
          this.source = this.sources[i];
        }
      }
      this.$emit('sourceChanged', e.target.value);
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.SourceSelection{
    padding: 5rem;
}

.p-side-2{
  padding: 0rem 1rem;
}

.p-top-1{
  padding-top: 1rem;
}


</style>
