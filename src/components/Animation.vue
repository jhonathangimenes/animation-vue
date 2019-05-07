<template>
    <div>
        <div class="jumbotron">
            <h1 class="display-4">Animantion Vue!</h1>
        </div>
        <div class="container">
            <div>
                <button class="btn btn-primary mb-4" @click.prevent="mostrar = !mostrar">Mudar</button>
                <transition appear name="fade">
                    <div class="alert alert-primary" v-if="mostrar"> Animação</div>
                </transition>
            </div>
             <div>
                <button class="btn btn-danger mt-4 mb-4" @click.prevent="mostrar2 = !mostrar2">Mudar</button>
                <transition appear name="zoom">
                    <div class="alert alert-danger" v-if="mostrar2"> Animação</div>
                </transition>
            </div>
            <div>
                <button class="btn btn-success mt-4 mb-4" @click.prevent="mostrar3 = !mostrar3">Mudar</button>
                <transition appear name="slide">
                    <div class="alert alert-success" v-if="mostrar3"> Animação</div>
                </transition>
            </div>
            <div>
                <button class="btn btn-warning mt-4 mb-4" @click.prevent="mostrar4 = !mostrar4">Mudar</button>
                <transition 
                appear
                    appear-active-class="animated flash"
                    enter-active-class="animated bounceIn"
                    leave-active-class="animated bounceOut"
                >
                    <div class="alert alert-warning" v-if="mostrar4"> Animação</div>
                </transition>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            mostrar: true,
            mostrar2: true,
            mostrar3: true,
            mostrar4: true
        }
    }
}
</script>

<style scoped>

    .fade-enter, .fade-leave-to  {
        opacity: 0;
    }

    .fade-enter-active, .fade-leave-active {
        transition: opacity 1s;
    }

    .fade-enter-to, .fade-leave {
        opacity: 1;
    }

    .zoom-enter, .zoom-leave-to {
        transform: scale(0);
    }

    .zoom-enter-active, .zoom-leave-active {
        transition: transform 0.5s;
    }

    .zoom-to-active, .zoom-leave {
        transform: scale(1);
    }

    .slide-enter, .slide-leave-to {
        opacity: 0;
    }

    .slide-enter-active {
        animation: slides 0.7s;
        transition: opacity 0.7s;
    }

    .slide-enter-to, .slide-leave {
        opacity: 1;
    }

    .slide-leave-active {
        animation: slides 0.7s reverse;
        transition: opacity 0.7s;
    }

    @keyframes slides {
        0% {
            transform: translateX(-100px);
        }
        100% {
            transform: translateX(0px);
        }
    }

</style>