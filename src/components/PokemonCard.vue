<template>
    <img v-bind:src="imageURL">
</template>

<script>
export default {
    name: 'pokemon-card',
    props: {
        imageURL: String
    }
}
</script>