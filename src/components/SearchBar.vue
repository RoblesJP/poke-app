<template>
    <form id="search">
        <input 
        :value="modelValue" 
        @input="$emit('update:modelValue', $event.target.value)" />
    </form>
</template>

<script>
export default {
    props: {
        modelValue: String
    }
}
</script>