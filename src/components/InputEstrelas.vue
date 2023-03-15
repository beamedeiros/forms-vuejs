<template>
<div>
    <i v-for="estrela in estrelas" :key="estrela.id" :class="estrela.estilo" @click="marcarAvaliacao(estrela.id)"></i>
</div>
</template>

<script>
export default {
    name: 'InputEstrelas',
    props: {
        numeroEstrelas: {
            type: Number,
            required: true
        }
    },
    data: () => ({
        estrelas: [],
        avaliacao: 0
    }),
    created(){
        this.iniciarEstrela()
    },
    methods: {
        iniciarEstrela() {
            for(let i=0; i < this.numeroEstrelas; i++){
                this.estrelas[i] = {id: i, estilo: 'bi bi-star estrela'}
            }
        },
        marcarAvaliacao(e) {
            this.iniciarEstrela()

            this.avaliacao = e + 1

            for(let i = 0; i < this.avaliacao; i++) {
                this.estrelas[i].estilo = 'bi bi-star-fill estrela preenchida'
            }

            //enviar um evento personalizado para o componente pai 
            this.$emit('avaliar', this.avaliacao)
            // this.$emit('updateAvaliar', this.avaliacao)
        }
    }
}
</script>

<style scoped>
.estrela {
    font-size: 1.5rem;
    color: #999;
    margin-left: 1px;
    margin-right: 1px;
}

.preenchida {
    color: #FC0;
}
</style>