<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <Botao id="btnIniciarContador" :labelBotao="botaoIniciar.label" :classIcon="botaoIniciar.classeIcone"
            @click="iniciar" :disabled="cronometroRodando" />
        <Botao id="btnFinalizarContador" :labelBotao="botaoFinalizar.label" :classIcon="botaoFinalizar.classeIcone"
            @click="finalizar" :disabled="!cronometroRodando" />
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue'
import Botao from './Botao.vue'

export default defineComponent({
    name: 'TemporizadorVue',
    components: {
        Cronometro,
        Botao
    },
    emits: ['aoTemporizadorFinalizado'],
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
            botaoIniciar: { label: 'play', classeIcone: 'fas fa-play' },
            botaoFinalizar: { label: 'stop', classeIcone: 'fas fa-stop' }
        }
    },
    computed: {
        tempoDecorrido(): string {
            return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11, 8)
        }
    },
    methods: {
        iniciar(): void {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => { this.tempoEmSegundos += 1 }, 1000)
        },
        finalizar(): void {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>
