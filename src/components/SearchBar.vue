<script>
import axios from 'axios';
export default {
    data() {
        return {
            
        }
    },
}
</script>

<template>
    <div>
        <label for="searchInp">Pokemon Name</label>
        <input type="text" id="searchInp" v-model="pokemonInp">
        <button type="submit" class="btn btn-outline-primary">search</button>
    </div>
</template>

<style lang="scss" scoped>
    
</style>