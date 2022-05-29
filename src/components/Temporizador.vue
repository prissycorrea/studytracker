<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>
                play
            </span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>
                stop
            </span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import Cronometro from './Cronometro.vue'
export default defineComponent({
    name: 'Temporizador-N',
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Cronometro
    },
    data () {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: { /*funcoes que ele é capaz de executar dada a interação do usuario*/
    iniciar () { /*quando o user clicar em play, começar a contagem*/
    /*1seg = 1000 ms */
    this.cronometroRodando = true
        this.cronometro = setInterval(() => {
            this.tempoEmSegundos += 1
        }, 1000) /*método do js em ms*/
    },
    finalizar () { //quando o user clicar em stop
        this.cronometroRodando = false
        clearInterval(this.cronometro)
        this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
        this.tempoEmSegundos = 0
    }
    }
})
</script>