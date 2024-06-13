  <template>
    <div class="grid-container calculator">
        <DisplayCalculadora :textDisplay="display" class="positionDisplay" />
    
        <BtnCalculadora v-for="button in buttons" :key="button.value" :value="button.value" :class="button.styleButton" @click="actionBtn"/>
    </div>
  </template>
  
  <script>
  import BtnCalculadora from './Btn.vue'
  import DisplayCalculadora from './Display.vue'
  
  export default {
    // eslint-disable-next-line
    name: 'Calculadora',
    components: {
      BtnCalculadora,
      DisplayCalculadora
    },
    data() {
      return {
        buttons: [
            { value: 1, styleButton: ''},
            { value: 2, styleButton: ''},
            { value: 3, styleButton: ''},
            { value: '+', styleButton: ''},
            { value: 4, styleButton: ''},
            { value: 5, styleButton: ''},
            { value: 6, styleButton: ''},
            { value: '-', styleButton: ''},
            { value: 7, styleButton: ''},
            { value: 8, styleButton: ''},
            { value: 9, styleButton: ''},
            { value: '*', styleButton: ''},
            { value: '.', styleButton: ''},
            { value: 0, styleButton: ''},
            { value: '=', styleButton: 'resultButton'},
            { value: '/', styleButton: ''},
            { value: 'Clear', styleButton: 'doubleButton'},
            { value: 'Delete', styleButton: 'doubleButton' }
        ],
        display: ''
      }
    },
    methods: {
        actionBtn(event) {
            if(event.target.value === '=') {
            const members = this.convertMenbersToNumbers(this.sliceExpressionMembers(this.display))
            this.display = this.calculate(members)
            return
            }
            if(event.target.value === 'Delete') {
            this.display = this.display.slice(0, -1)
            return
            }
            if(event.target.value === 'Clear') {
            this.display = ''
            return
            }
            this.display += event.target.value
        },
        //método para recortar os numeros da expressão, pegar somente os números
        sliceExpressionMembers(expression) {
            const members = expression.split(/(\+|\-|\*|\/)/g)
            return members
        },
        convertMenbersToNumbers(members) {
            return members.map(member => {
                if(isNaN(member)) {
                    return member
                }
                return Number(member)
            })
        },
        calculate(members) {
            //retorna index do operador * ou /
            let index = members.findIndex(member => member === '*' || member === '/')

            if(index !== -1) {
                let result = 0
                switch(members[index]) {
                    case '*':
                    result = members[index - 1] * members[index + 1]
                    break
                    case '/':
                    if(members[index + 1] === 0) {
                        return 'Error'
                    }
                    result = members[index - 1] / members[index + 1]
                    break
                }
                members.splice(index - 1, 3, result)
                return this.calculate(members)
            }

            //retorna index do operador + ou -
            index = members.findIndex(member => member === '+' || member === '-')
            if(index !== -1) {
                let result = 0
                switch(members[index]) {
                    case '+':
                    result = members[index - 1] + members[index + 1]
                    break
                    case '-':
                    result = members[index - 1] - members[index + 1]
                    break
                }
                members.splice(index - 1, 3, result)
                return this.calculate(members)
            }
            //retorna o resultado com 2 casas decimais
            return members[0].toFixed(2).toString()
        }
        
    }
  }
  </script>
  
  <style scoped>
    .calculator {
        border: 2px solid black;
        padding: 1rem;
        border-radius: 0.5rem;
        background-color: #4b4b4b;
        margin: 0.5rem;
        box-shadow: -18px 22px 24px -4px rgba(0,0,0,0.5),0px 10px 15px -3px rgba(0,0,0,0.1);
    }

    .grid-container {
        display: grid;
        justify-content: space-between;
        align-content: center;
        grid-template-columns: 1fr 1fr 1fr 0.5fr;
        grid-template-rows: 2fr 1fr 1fr 1fr 1fr;
    }

    .positionDisplay {
        grid-column: 1 / 5;
    }

    .doubleButton {
        grid-column: span 2;
    }

    .resultButton {
        background-color: orange;
        color: white;
    }
  </style>
  