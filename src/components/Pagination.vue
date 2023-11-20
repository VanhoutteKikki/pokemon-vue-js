<template>
    <div class="c-pages">
        <button class="c-pages__action">
            <ChevronLeft class="c-pages__icon" />
        </button>

        <p class="c-pages__current"></p>
        <p class="c-pages__divider"></p>
        <p class="c-pages__total">{{ 195 }}</p>

        <button class="c-pages__action">
            <ChevronRight class="c-pages__icon" />
        </button>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const currentPage = ref(1)

</script>

<styles lang="scss">
// .c-pages {
//     display: flex;
// }
</styles>