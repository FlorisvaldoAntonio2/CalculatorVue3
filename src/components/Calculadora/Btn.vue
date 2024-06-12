<template>
    <button class="btn" :value="value">
        {{value}}
    </button>
</template>

<script>
    export default {
        name: 'BtnCalculadora',
        props: {
            value: {
                type: [Number, String],
                required: true
            }
        }
    }
</script>

<style scoped>
    .btn {
        background-color: #f1f1f1;
        border: none;
        border-radius: 5px;
        color: #333;
        cursor: pointer;
        font-size: 1.5rem;
        padding: 1rem 1rem;
        margin: 0.2rem;
    }
</style>