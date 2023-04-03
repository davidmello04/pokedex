<template>
  <div id="app">

    <div id="nav">
      <div id="logo">
        <a href="/">
          <img src="./assets/img/logo-principal.png" id="logo-icon" alt="pokebola">
        </a>
      </div>
      <div id="div-search">
        <img src="./assets/img/pikachu.png" id="pikachu" alt="pikachu">
        <input id="search" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" @keydown.enter="buscar">
        <button class="button is-medium is-info" id="btnSearch" @click="buscar">Buscar</button>
      </div>
    </div>

    <div id="stripe"></div>
    <div id="title">
      <h1 id="title-description">Cards de Pokemons</h1>
      <div id="stripe-title"></div>
    </div>

    <div id="div-column" class="columns is-multiline">
      <div id="columns-cards" class="column is-one-quarter" v-for="(poke, index) in paginatedPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="(currentPage - 1) * pageSize + index + 1" />
      </div>
    </div>

    <div id="pagination" class="pagination" role="navigation" aria-label="pagination">
      <div id="buttons-pagination">
        <button id="btn-pag" class="pagination-previous" :disabled="currentPage === 1" @click="prevPage">Anterior</button>
        <button class="pagination-next" :disabled="currentPage === pageCount" @click="nextPage">Próxima</button>
      </div>
      <ul class="pagination-list">
        <li><a class="pagination-link" :class="{ 'is-current': page === currentPage }" v-for="page in pages" :key="page"
            @click="changePage(page)">{{ page }}</a></li>
      </ul>
    </div>

    <Footer :author="author" :profession="profession" />

  </div>
</template>

<script>
import axios from "axios"
import Pokemon from "./components/Pokemon.vue"
import Footer from "./components/Footer.vue"

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filterPokemons: [],
      busca: "",
      author: "David Melo",
      profession: "Programador",
      pageSize: 27,
      currentPage: 1
    }
  },

  created: function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista de pokemons")
      console.log(res)
      this.pokemons = res.data.results
      this.filterPokemons = res.data.results
    }).catch()
  },

  components: {
    Pokemon,
    Footer
  },

  methods: {
    buscar: function () {
      this.filterPokemons = this.pokemons
      this.filterPokemons = this.busca.trim().toLowerCase() === ''
        ? this.pokemons
        : this.pokemons.filter(pokemon => pokemon.name.toLowerCase().startsWith(this.busca.toLowerCase()))
      this.currentPage = 1
    },
    prevPage() {
      this.currentPage -= 1
    },
    nextPage() {
      this.currentPage += 1
    },
    changePage(page) {
      this.currentPage = page
    }
  },

  computed: {
    pageCount() {
      let itemCount = this.filterPokemons.length
      let pageCount = Math.ceil(itemCount / this.pageSize)
      return pageCount
    },
    pages() {
      let pages = []
      for (let i = 1; i <= this.pageCount; i++) {
        pages.push(i)
      }
      return pages
    },
    paginatedPokemons() {
      let startIndex = (this.currentPage - 1) * this.pageSize
      let endIndex = startIndex + this.pageSize
      return this.filterPokemons.slice(startIndex, endIndex)
    }
  },
}
</script>

<style scoped>
#app {
  max-width: auto;
  min-width: 99%;
  margin: 0 auto;
}

/* NAVEGAÇÃO */
#nav {
  width: 100%;
  height: auto;
  padding: 1rem;
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  background-color: rgb(0, 105, 204);
}

/* LOGO */
#logo {
  width: auto;
  margin-bottom: 1rem;
}

#logo-icon {
  width: auto;
  max-width: 38%;
}

/* BUSCA */
#div-search {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-width: 38%;
  margin: 0;
}

#pikachu {
  width: 7rem;
  margin-right: 1rem;
}

#btnSearch {
  height: 2.5rem;
  background-color: red;
  margin-left: 0.5rem;
}

#search {
  height: 2.9rem;
  padding: 1rem;
  border-radius: 1.25rem;
  width: 100%;
  border: 2px solid rgb(4, 98, 187);
}

#search:focus {
  outline: none;
  border: 1px solid rgb(5, 79, 148);
  background-color: aliceblue;
}

#btnSearch:hover {
  background-color: rgb(158, 0, 0);
}

/* LINHA */
#stripe {
  background-color: rgb(0, 105, 204);
  height: 1rem;
  margin-top: 1.5rem;
  width: 100%;
}

/* TÍTULO */
#title {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 1.5rem 1.5rem 0.5rem 1.5rem;
}

#title-description {
  font-size: 2.69em;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: bold;
  text-transform: uppercase;
  color: aliceblue;
  width: 100%;
}

#stripe-title {
  background-color: rgb(158, 0, 0);
  height: 0.25rem;
  width: 21%;
}

/* COLUNAS */
#div-column {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  padding: 1rem;
}

#columns-cards {
  margin: 1rem;
}

/* PAGINAÇÃO */
#pagination {
  display: flex;
  flex-direction: column-reverse;
}

#buttons-pagination {
  display: flex;
  margin: 1.5rem;
}

button {
  cursor: pointer;
}
</style>
