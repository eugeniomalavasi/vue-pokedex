<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                baseUrl: 'https://pokeapi.co/api/v2/pokemon',
                pokemonInp: null,
                results: []
            }
        },
        created() {
            const localPokedex = localStorage.getItem("pokedex");
            if (localPokedex) {
                this.results = JSON.parse(localPokedex) || [];
            }
        },
        methods: {
            pokeSearch() {
                axios
                    .get(`${this.baseUrl}/${this.pokemonInp.toLowerCase()}`)
                    .then(resp => {
                        const newPokemon = resp.data;

                        this.results.push(newPokemon);

                        localStorage.setItem("pokedex", JSON.stringify(this.results));

                        this.pokemonInp = '';
                    })
                    .catch(error => {
                        console.error("Error fetching the Pokémon data:", error);
                    });
            },
            pokeDelete(index) {
                this.results.splice(index,1);
                localStorage.setItem("pokedex", JSON.stringify(this.results));
                console.log('deleted');
                
            }
        },
    }
</script>

<template>
    <div class="container">
        <div class="">
            <label for="searchInp">Pokemon Name</label>
            <input type="text" id="searchInp" v-model="pokemonInp">
            <button type="submit" @click="pokeSearch()" class="btn btn-outline-primary">Search</button>
        </div>

        <div class="row">
            <div class="col-md-3 mt-3 p-2 border border-black rounded" v-for="(pokemon, index) in results" :key="index">
                <img :src="pokemon.sprites.front_default" class="card-img-top" :alt="pokemon.name">
                <div class="card-body row">
                    <h5 class="card-title">{{ pokemon.name }}</h5>
                    <div v-for="(stat, statIndex) in pokemon.stats" :key="statIndex">
                        <div class="progress mt-1 mb-1" role="progressbar" aria-label="stats" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100">
                            <div class="progress-bar" :style="{ width: stat.base_stat + '%' }">{{ stat.stat.name }}: {{ stat.base_stat }}</div>
                        </div>
                    </div>
                </div>
                <button type="submit" class="btn btn-danger" @click="pokeDelete(index)">delete</button>
            </div>
        </div>
    </div>


</template>


<style lang="scss" scoped>

</style>