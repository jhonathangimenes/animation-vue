<template>
    <form @submit.prevent="mark()">
        <label>Paciente</label>
        <input class="form-control"
            type="text"
            placeholder="Nome paciente"
            v-model.lazy.trim="patient.name">
        <label>Idade</label>
        <input class="form-control"
            type="number"
            placeholder="Idade do paciente"
            v-model="patient.age">
        <label>Horario do atendimento</label>
        <select class="form-control" v-model="patient.schedule">
            <option selected= disabled value="">Selecione horario...</option>
            <option value="9:00">9:00</option>
            <option value="10:00">10:00</option>
            <option value="11:00">11:00</option>
            <option value="12:00">12:00</option>
        </select>
        <div class="float-right mt-3">
            <button class="btn btn-secondary mr-2" @click="$emit('back')">Cancelar</button>
            <button class="btn btn-success">Salvar</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            patient: {
                id: 0,
                name: '',
                age: undefined,
                schedule: ''
            }
        }
    },
    methods: {
        mark() {
            this.$emit('markForm', this.patient)
            this.patient = {}
        }
    }
}
</script>

<style>

</style>


