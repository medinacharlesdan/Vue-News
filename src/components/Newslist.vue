<template>
  <div class="Newslist ui container">
    <h1 class="ui header ">News List</h1>

    <div class="ui three column grid" >
        <div class="column" v-for="article in articles">
        
                <div class="ui card">
                <div class="image">
                <img :src="article.urlToImage">
                </div>
                <div class="content">
                <a class="header">{{article.title}}</a>
                <div class="meta">
                <span class="date">{{article.publishedAt}}</span>
                </div>
                <div class="description">
                {{article.description}}
                </div>
                </div>
                <div class="extra content">
                {{article.author}}
               <span class="right floated star">
                   <a :href="article.url" target="_blank">
                <i class="newspaper icon"></i>
                Read more
                </a>
                </span>
                </div>
                </div>
        </div>
       
    </div>
  </div>
</template>




<script>
export default {
 name: 'Newslist',
 props:['source'],
 data (){
     return{
     articles:[],
    article:""
     }
 },
 methods:{
     updateSource: function(source){
         this.$http.get("https://newsapi.org/v2/everything?sources="+ source +"&language="+ "en" +"&page"+20+"&apiKey=e56ad3527e184b7c82638f3a7b47c92b").then(
             response => {
                 this.articles = response.data.articles;
             });
     }
 },
 watch:{
     source: function(val){
         this.updateSource(val);
     }
 },created:function(){
     this.updateSource(this.source);
 }
 
}
</script>

<style scoped>
.Newslist{
    padding:0rem 5rem;
}

</style>
