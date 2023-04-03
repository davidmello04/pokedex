<template>
    <div id="card" class="card">
        <div class="card-image">
            <h2 id="name-card">CARD - {{ upper }}</h2>
            <figure id="pokemon">
                <img id="img-pokemon" :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div id="card-content" class="card-content">
            <div class="media">
                <div class="media-content">
                    <p id="name" class="name title is-5">
                        <span id="number-poke">{{ num }}</span>
                        <img src="../assets/img/pokebola.png" alt="pokebola" id="pokebola">
                        <span id="pokemon-name">
                            {{ upper }}
                        </span>
                    </p>
                    <p class="description-card bold is-6">
                        Tipo:&nbsp;
                        <span v-for="(type, index) in pokemon.types" :key="index">
                            {{ type }} <span v-if="index !== pokemon.types.length - 1">/&nbsp;</span>
                        </span>
                    </p>
                    <p class="description-card bold is-6">
                        Altura: {{ pokemon.height }} m
                    </p>
                    <p class="description-card bold is-6">
                        Peso: {{ pokemon.weight }} kg
                    </p>
                    <p class="description-card bold is-6">
                        Habilidades:&nbsp;
                        <span v-for="(ability, index) in pokemon.abilities" :key="index">
                            {{ ability }} <span v-if="index !== pokemon.abilities.length - 1">/&nbsp;</span>
                        </span>
                    </p>
                </div>
            </div>
            <div class="content">
                <button id="btn" class=" button is-medium is-fullwidth is-info" @click="mudarSprite">SPIN POKEMON
                </button>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from "axios"

export default {
    created: function () {
        axios.get(this.url).then(res => {
            console.log(res)
            let types = res.data.types.map(type => type.type.name)
            this.pokemon.types = types
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.pokemon.height = res.data.height / 10
            this.pokemon.weight = res.data.weight / 10
            let abilities = res.data.abilities.map(ability => ability.ability.name)
            this.pokemon.abilities = abilities
            this.currentImg = this.pokemon.front
        })
    },

    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                types: [],
                front: '',
                back: '',
                height: '',
                weight: '',
                abilities: []
            }
        }
    },

    props: {
        num: Number,
        name: String,
        url: String
    },

    computed: {
        upper() {
            var newName = this.name.toUpperCase()
            return newName
        }
    },

    methods: {
        mudarSprite: function () {
            if (this.isFront) {
                this.isFront = false
                this.currentImg = this.pokemon.back
            } else {
                this.isFront = true
                this.currentImg = this.pokemon.front
            }
        }
    }
}
</script>

<style>

  @import url('https://fonts.googleapis.com/css2?family=Bubbler+One&family=Comic+Neue&family=Montserrat&family=Oswald:wght@300&family=Roboto+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');




#card {
    border: 20px solid #214468;
    border-radius: 0.25rem;
}

#card:hover {
    box-shadow: 0 0 20px 10px #c20d0d;
}

#name-card {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: red;
    color: white;
    justify-content: center;
    text-align: center;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    font-size: large;
    height: 2.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
}

#pokemon {
    display: flex;
    align-items: center;
    justify-content: center;
}

#img-pokemon {
    width: 10rem;
}

#card-content {
    overflow: hidden;
}

#name {
    background-color: #214468;
    display: flex;
    justify-content: flex-start;
    margin-bottom: 2rem;
}

#number-poke {
    background-color: rgb(0, 105, 204);
    color: white;
    padding: 0.5rem;
    border-radius: 3px;
}

#pokebola {
    width: 2rem;
    margin: 1rem;
}

#pokemon-name {
    color: white;
}

.description-card {
    display: flex;
    justify-content: flex-start;
    font-family: 'Comic Neue', 'Oswald', sans-serif;
    text-transform: uppercase;
    padding: 0.5rem;
    margin-top: 0.25rem;
    border-left: solid 0.4rem rgb(0, 105, 204);
    border-bottom: solid 0.3rem rgb(0, 105, 204);
    white-space: nowrap;
}

p {
    background-color: rgba(77, 77, 78, 0.171);
    height: 2.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.bold {
    font-weight: bold;
}

#btn {
    font-weight: 600;
}
</style>