<template>
    <div id="pokemon">
        <div class="card">
        <div class="card-image">
            <figure>
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{id}} - {{name | upper}}</p>
                <p class="subtitle is-size-7"> tipo:{{ pokemon.type }}  | altura:{{ height }} | peso:{{ weight }} </p>
            </div>
            </div>
            <div class="content">
                <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
            </div>
        </div>
        </div>


    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            this.id = res.data.id;
            this.height = res.data.height;
            this.weight = res.data.weight
        })
    },
    data(){
        return {
            isFront: true,
            currentImg : '',
            pokemon: {
                type: '',
                front: '',
                back: '',
                id: '',
                height: '',
                weight: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    computed: {
        upper(value){
            var newName = value[0].toUpperCase();
            return newName;
        }
    },
    methods: {
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
 #pokemon{
    margin-top: 3%;
    width: 100%;
 }
</style>