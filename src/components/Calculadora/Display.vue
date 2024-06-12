<template>
    <div class="display">
        <input type="text" class="display_input" readonly :value="displayFormated" />
    </div>
</template>

<script>
    export default {
        name: 'DisplayCalculadora',
        props: {
            textDisplay: {
                type: String,
                required: true
            }
        },
        computed: {
            displayFormated() {
                //sempre que encontrar um operador, adicione um espaço antes e depois
                return this.textDisplay.replace(/(\+|\-|\*|\/)/g, ' $1 ')
            }
        }
    }
</script>

<style scoped>
    .display {
        background-color: #333;
        color: #fff;
        font-size: 2rem;
        padding: 2rem;
        text-align: right;
        border-radius: 0.5rem;
        margin-bottom: 1rem;
    }
    .display_input {
        background-color: transparent;
        border: none;
        color: inherit;
        font-size: 3rem;
        text-align: right;
        width: 100%;
        font-family: 'DigitalFont';
    }
</style>