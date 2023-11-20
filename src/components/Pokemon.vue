//pokemon.vue
<template>
    <div class="c-pokemon">
        <img class="c-pokemon__img" :src="getPokemonImageUrl()" :alt="`avatar van ${pokemonData.name}`" />
        <div class="c-pokemon__info">
            <div class="c-pokemon__header">
                <h1 class="c-pokemon__name">{{ pokemonData.name }}</h1>
                <label :for="pokemonData.name" class="c-pokemon-spin">
                    <input v-model="showBack" :id="pokemonData.name" type="checkbox" class="c-pokemon-spin__input sr-only" />
                    <RefreshCw v-if="showBack" class="c-pokemon-spin__icon" />
                    <RefreshCcw v-else class="c-pokemon-spin__icon" />
                </label>
                <span class="sr-only">Toggle Pokemon from back to front and vice verse.</span>
            </div>

            <p class="c-pokemon__link">More info
                <ChevronRight />
            </p>
            <!-- <p class="c-pokemon__checkbox"><input class="c-pokemon__input" type="checkbox" /></p> -->
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { RefreshCcw, RefreshCw, ChevronRight } from 'lucide-vue-next';
const props = defineProps({
    pokemonData: {
        type: Object,
        required: true,
    },
});

const showBack = ref(false);

const getPokemonid = function () {
    const partOfUrl = props.pokemonData.url.split('/');

    return partOfUrl[partOfUrl.length - 2];
};

const getPokemonImageUrl = function () {
    const baseUrl = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated`
    if (showBack.value) {
        return `${baseUrl}/back/${getPokemonid()}.gif`
    }
    return `${baseUrl}/${getPokemonid()}.gif`;
};
</script>

<style lang="scss">
.c-pokemon {
    width: 100%;

    @media(min-width: 480px) {
        width: calc((100% - 1 * 2rem)/2);
    }

    @media(min-width: 768px) {
        width: calc((100% - 3 * 2rem)/4);
    }

    &__link {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        padding: 1rem 0;
        font-size: .75rem;
        margin: 0 0 0 auto;
        text-decoration: underline;
    }

    &__img {
        height: 7rem;
        width: auto;
        display: block;
        margin-bottom: -0.5rem;
    }

    &__info {
        display: flex;
        flex-direction: column;
        background: #444;
        color: #fff;
        padding: .5rem 1rem;
        border-radius: 1rem 2rem 1rem 2rem;
    }

    &__header {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    &__name {
        font-size: 1.5rem;
        font-weight: 600;
        margin: 0;
        text-transform: capitalize;
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

    &:focus-within {
        outline: 3px solid lightcyan;
    }
}

.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border-width: 0;
}
</style>