<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex" @submit.prevent>
            <input type="text" 
            class="form-control new-movie-label" 
            placeholder="yangi kino qo'shing"
             :value='name'
             @input="name = $event.target.value"/>
            <input type="number" 
            class="form-control new-movie-label" 
            placeholder="nechi maratoba ko'rilgan" 
            :value="viewers"
            @input="viewers = $event.target.value"/>
            <button class="btn btn-outline-dark" type="submit" @click="addMovie">Q'shish</button>
        </form>
    </div>
</template>
<script>
export default {
    data(){
        return{
            name:'',
            viewers:''
        }
    },
    methods:{
        addMovie(){
            if(!this.name || !this.viewers) return
            const newMovie = {
             name: this.name,
             viewers:this.viewers,  
             favourite: true,
             like: false,
             id: Date.now()
          }
          this.$emit('createMovie',newMovie)   //bola divdan ona divga ma'lumot berish
          this.name = ''
          this.viewers = ''
          console.log(newMovie)
        }
    }
}
</script>
<style scoped>
    .movie-add-form{
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px,15px,15px rgb(0, 0, 0,0.15);
    }
</style>