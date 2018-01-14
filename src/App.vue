<template>
  <div id="app" class="ui container">
   <SourceSelection @sourceChanged="sourceChanged"></SourceSelection>
   <Newslist :source="source"></Newslist>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection'
import Newslist from './components/Newslist'

export default {
  name: 'app',
  components: {
    SourceSelection,
    Newslist
  },
  data(){
    return{
      source:"",

    }
  },
  methods:{
    sourceChanged: function(source){
      this.source = source;
    }
  }
}
</script>

<style>


</style>
