<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                baseUrl: 'https://pokeapi.co/api/v2/pokemon',
                pokemonInp: null,
                results: [] // Make sure it's an array initially
            }
        },
        created() {
            // Retrieve the pokedex from localStorage
            const localPokedex = localStorage.getItem("pokedex");
            if (localPokedex) {
                // Parse localStorage data and ensure it's an array
                this.results = JSON.parse(localPokedex) || [];
            }
        },
        methods: {
            pokeSearch() {
                axios
                    .get(`${this.baseUrl}/${this.pokemonInp.toLowerCase()}`)
                    .then(resp => {
                        const newPokemon = resp.data;

                        // Push new Pokémon data to the results array
                        this.results.push(newPokemon);

                        // Save the updated array to localStorage
                        localStorage.setItem("pokedex", JSON.stringify(this.results));

                        // Clear the input field
                        this.pokemonInp = '';
                    })
                    .catch(error => {
                        console.error("Error fetching the Pokémon data:", error);
                    });
            }
        },
    }
</script>

<template>
    <div>
        <label for="searchInp">Pokemon Name</label>
        <input type="text" id="searchInp" v-model="pokemonInp">
        <button type="submit" @click="pokeSearch()" class="btn btn-outline-primary">Search</button>
    </div>

    <div v-for="(pokemon, index) in results" :key="index" class="card mt-4" style="width: 18rem;">
        <img :src="pokemon.sprites.front_default" class="card-img-top" :alt="pokemon.name">
        <div class="card-body">
            <h5 class="card-title">{{ pokemon.name }}</h5>
            <div class="container">
                <div class="row">
                    <div class="col" v-for="(stat, statIndex) in pokemon.stats" :key="statIndex">
                        {{ stat.stat.name }}: {{ stat.base_stat }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<style lang="scss" scoped>

</style>