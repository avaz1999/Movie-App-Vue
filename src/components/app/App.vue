<template>
    <div class="app app-monospace">
        <div class="content">
            <AppInfo :allMoviesCount="movies.length" :favouriteMovieCount="movies.filter(c => c.favourite).length"/>
            <div class="search-panel">
                <SearchPanel/>
                <AppFilter/>
            </div>
            <MovieList :movies="onSearchHandler(movies,term)"
             @onTogle="onTogleHandler"
             @onRemove="onRemoveHandler"/>
            <MovieAddFrom @createMovie="createMovie"/>
        </div>
    </div>
</template>
<script>
import AppInfo from "@/components/app-info/AppInfo.vue"
import SearchPanel from "../search-panel/SearchPanel.vue"
import AppFilter from "../app-filter/AppFilter.vue"
import MovieList from "../movie/MovieList.vue";
import MovieAddFrom from "../movie/MovieAddFrom.vue";
export default{
    components:{AppInfo,SearchPanel,AppFilter,MovieList,MovieAddFrom},
    data(){
        return {
            movies:[
                {
                    name: "Spider Man",
                    viewers:82,
                    favourite:true,
                    like: true,
                    id: 1
                },
                {
                    name: "Jumong",
                    viewers:543,
                    favourite:false,
                    like: false,
                    id: 2                    
                },
                {
                    name: "Dengiz Hukumdori",
                    viewers:56 ,
                    favourite:false,
                    like: false,
                    id: 3
                }
            ],
            term: ''
        }
    },

    methods:{
        createMovie(item){
            this.movies.push(item)
        
        },
        onTogleHandler({id,prop}){
           this.movies = this.movies.map(item =>{
                if(item.id === id){
                    console.log(item)
                    return {...item, [prop] : !item[prop]}  //spread operatori obektdan clone qilib beradi
                }
                return item
            })
        },
        onRemoveHandler(id){
            this.movies = this.movies.filter(c => c.id != id)
        },
        onSearchHandler(arr, term){
            if(term.length == 0){
                return arr
            }
            return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
        },
        updateTermHandler(term){
            this.term = term
        }        
    }
}

</script>
<style>
.app{
    height: 100vh;
    color: #000;
}
.content{
    width: 1200px;
    min-height: 900px;
    background-color: #fff;
    margin: 0 auto;
    padding: 5rem 0;
}
.search-panel{
        margin-top: 2rem;
        padding: 1.5rem;
        background-color: #fcfaf5;
        border-radius: 4px;
        box-shadow: 15px,15px,15px rgb(0, 0, 0,0.15);
}
</style>