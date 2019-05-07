<template>
    <div>
        <div class="jumbotron">
            <h1 class="display-4">Animantion Vue!</h1>
        </div>
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <form @submit.prevent="mark">
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
                            <option selected disabled value="">Selecione horario...</option>
                            <option value="9:00">9:00</option>
                            <option value="10:00">10:00</option>
                            <option value="11:00">11:00</option>
                            <option value="12:00">12:00</option>
                        </select>
                        <div class="float-right mt-3">
                            <button class="btn btn-secondary mr-2">Cancelar</button>
                            <button class="btn btn-success">Salvar</button>
                        </div>
                    </form>
                </div>
                <div class="col-md-6">
                    <transition-group name="list" 
                        class="list-group" tag="ul">
                        <li class="list-group-item"
                            v-for="consultation in consultations" 
                            :key="consultation.id">
                            <strong>Paciente:</strong> {{ consultation.name }}
                            <strong>Idade:</strong> {{ consultation.age }}
                            <strong>Horario:</strong> {{ consultation.schedule }}
                            <button class="btn btn-danger float-right" @click="remove(consultation)">X</button>
                        </li>
                    </transition-group>
                </div>
            </div>
        </div>
    </div>
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
            },
            consultations: [
                {id: 1, name: 'João', age: '38', schedule: '9:00'},
                {id: 2, name: 'Pedro', age: '22', schedule: '10:00'},
                {id: 3, name: 'Maria', age: '59', schedule: '11:00'},
                {id: 4, name: 'Rafael', age: '13', schedule: '12:00'}
            ]
        }
    },
    methods: {
        mark() {
            this.patient.id = +this.consultations.length + 1
            this.consultations.push(this.patient)
            this.patient = {}
        },
        remove (consultation) {
            let index = this.consultations.indexOf(consultation);
            this.consultations.splice(index, 1)
        }
    }
}
</script>

<style scoped>
    .list-enter, .list-leave-to {
        opacity: 0;
        transform: translateX(-70px)
    }
    .list-enter-active, .list-leave-active {
        transition: all 0.5s;
    }

    .list-move {
        transition: all 0.5s;
    }

    .list-leave-active {
        position: absolute;
        width: calc(100% - 31px);
    }
</style>