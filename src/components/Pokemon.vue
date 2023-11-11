//pokemon.vue
<template>
    <div class="c-pokemon">
        <img class="c-pokemon__img" :src="getPokemonImageUrl()" :alt="`avatar van ${pokemonData.name}`" />
        <div class="c-pokemon__info">
            <h1 class="c-pokemon__name">{{ pokemonData.name }}</h1>
            <label for="" class="c-pokemon-spin">
                <input type="checkbox" class="c-pokemon-spin__input" />
                <RotateCw class="c-pokemon-spin__icon" />
                <RotateCcw class="c-pokemon-spin__icon" />
            </label>
            <p class="c-pokemon__info">More info
                <ChevronRight />
            </p>
            <!-- <p class="c-pokemon__checkbox"><input class="c-pokemon__input" type="checkbox" /></p> -->
        </div>
    </div>
</template>

<script setup>
import { RotateCcw, RotateCw, ChevronRight } from 'lucide-vue-next';
const props = defineProps({
    pokemonData: {
        type: Object,
        required: true,
    },
});

const getPokemonid = function () {
    const partOfUrl = props.pokemonData.url.split('/');

    return partOfUrl[partOfUrl.length - 2];
};

const getPokemonImageUrl = function () {
    return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getPokemonid()}.gif`;
};
</script>

<style lang="scss">
.c-pokemon {
    &__img {
        margin-bottom: -0.5rem;
        height: 7rem;
        width: auto;
    }

    &__info {
        background-color: #4f4f4f;
        border-radius: 2rem;
        width: 20%;
        padding: 2rem;
    }

    &__name {
        font-size: 1.5rem;
    }

    //   &__checkbox {
    //     display: flex;
    //     flex-shrink: 0;
    //     align-items: center;
    //     justify-content: center;
    //     background: #111111;
    //     border-radius: 50%;
    //     height: 3rem;
    //     width: 3rem;
    //     cursor: pointer;
    //     margin-left: 1rem;
    //     transition: background 0.2s ease-in-out;
    //     color: white;

    //     &:hover {
    //       background: #808080;
    //     }
    //   }

    &__input {
        display: none;
    }
}

.c-pokemon-spin {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    background: #111111;
    border-radius: 50%;
    height: 3rem;
    width: 3rem;
    cursor: pointer;
    margin-left: 1rem;
    transition: background 0.2s ease-in-out;
    color: white;

    &:hover {
        background: #808080;
    }

    &__input {
        display: none;
    }
}
</style>