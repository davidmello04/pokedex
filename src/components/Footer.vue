
<template>
    <footer>
        <img src="../assets/img/pokemons.png" id="img-footer" alt="">
        <p id="footer">
            Feito por {{ author }} - {{ profession }} | Utilizando a API pokeAPI.
        </p>
        <small>Os dados foram obtidos da <a href="https://pokeapi.co/" target="_blank">PokeAPI</a>, uma fonte pública de
            informações sobre Pokémon.</small>
    </footer>
</template>
  
<script>
export default {
    name: "Footer",
    props: {
        author: {
            type: String,
            required: true
        },
        profession: {
            type: String,
            required: true
        }
    }
}
</script>

<style>
footer {
    background-color: rgb(0, 105, 204);
    padding: 2rem 0 2rem 0;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    flex-direction: column;
}

img {
    width: 40%;
}

small a {
    color: rgb(5, 0, 82);
    font-weight: bold;
}

small {
    color: white;
    margin-top: 0.5rem;
}

#footer {
    font-size: 1rem;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    width: 100%;
    margin-top: 2rem;
}
</style>