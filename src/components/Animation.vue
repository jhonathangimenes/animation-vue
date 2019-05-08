<template>
    <div>
        <div class="jumbotron">
            <h1 class="display-4">Animation Vue!</h1>
        </div>
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <transition enter-active-class="animated rubberBand">
                        <component :is="status" 
                            @change="status = 'Form'"
                            @back="status = 'Start'"
                            @markForm="mark($event)">
                        </component>
                    </transition>
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
    components: {
        Form: () => import('./Form.vue'),
        Start: () => import('./Start.vue')
    },
    data() {
        return {
            status: 'Start',
            consultations: [
                {id: 1, name: 'João', age: '38', schedule: '9:00'},
                {id: 2, name: 'Pedro', age: '22', schedule: '10:00'},
                {id: 3, name: 'Maria', age: '59', schedule: '11:00'},
                {id: 4, name: 'Rafael', age: '13', schedule: '12:00'}
            ]
        }
    },
    methods: {
        mark(event) {
            event.id = +this.consultations.length + 1
            this.consultations.push(event)
            this.status = 'Start'
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