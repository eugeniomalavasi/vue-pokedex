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
        methods: {
            pokeSearch() {
                axios
                    .get(`${this.baseUrl}/${this.pokemonInp.toLowerCase()}`)
                    .then((resp => {

                        this.results = resp.data;
                        console.log(this.results);
                    }));

            },
        },
    }
</script>

<template>
    <div>
        <label for="searchInp">Pokemon Name</label>
        <input type="text" id="searchInp" v-model="pokemonInp">
        <button type="submit" @click="pokeSearch()" class="btn btn-outline-primary">search</button>
    </div>

    <div class="card" style="width: 18rem;" v-if="this.results!=''">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
            <h5 class="card-title">{{ this.results.name }}</h5>
            <div class="container">
                <div class="row">
                    <div class="col"> {{ this.results.stats[0].stat.name }} {{ this.results.stats[0].base_stat }}
                    </div>
                    <div class="col"> {{ this.results.stats[1].stat.name }} {{ this.results.stats[1].base_stat }}
                    </div>
                    <div class="col"> {{ this.results.stats[2].stat.name }} {{ this.results.stats[2].base_stat }}
                    </div>
                    <div class="col"> {{ this.results.stats[3].stat.name }} {{ this.results.stats[3].base_stat }}
                    </div>
                    <div class="col"> {{ this.results.stats[4].stat.name }} {{ this.results.stats[4].base_stat }}
                    </div>
                    <div class="col"> {{ this.results.stats[5].stat.name }} {{ this.results.stats[5].base_stat }}
                    </div>
                </div>
            </div>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
    </div>
</template>

<style lang="scss" scoped>

</style>