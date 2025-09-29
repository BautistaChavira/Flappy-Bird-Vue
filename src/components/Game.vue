<template>
    <div class="game" @click="startGame">
        <Bird :y="birdY" />
        <Pipe v-for="pipe in pipes" :key="pipe.id" :x="pipe.x" :gapY="pipe.gapY" />
        <div class="score">Score: {{ score }}</div>

        <!-- esto pone el texto de empezar -->
        <div v-if="!isStarted" class="start-text">Da click para empezar</div>
    </div>
</template>

<script>
import Bird from './Bird.vue'
import Pipe from './Pipe.vue'

export default {
    components: { Bird, Pipe },
    data() {
        //variables que controlan la logica basica del juego
        return {
        birdY: 200,
        velocity: 0,
        gravity: 0.5,
        pipes: [],
        score: 0,
        gameInterval: null,
        isStarted: false,
        }
        //no controlan la generacion de tubos ni sus posiciones
    },
    methods: {
        startGame() { // la logica de que el juego no comience automaticamente
            if (!this.isStarted) {
                this.isStarted = true
            }
            this.velocity = -8
        },
        updateGame() {
            if (!this.isStarted) return // esto mantiene el juego congelado al comienzo (otra vez)

            this.velocity += this.gravity
            this.birdY += this.velocity

            // esto mueve los tubos, alterando la posicion directamente
            this.pipes.forEach(pipe => pipe.x -= 2)

            // esto genera los tubos
            const lastPipe = this.pipes[this.pipes.length - 1]
            if (!lastPipe || lastPipe.x < 400) {
                const gapY = Math.random() * 500 + 150 // esto determina que tan verticalmente separados estaran
                const newX = lastPipe ? lastPipe.x + 300 : 600 // esto para lo horizontal
                this.pipes.push({
                    id: Date.now(),
                    x: newX,
                    gapY
                })
            }

            // esto elimina los tubos que se salen de pantalla
            this.pipes = this.pipes.filter(pipe => pipe.x > -50)

            // aca los eventos en funcion de si esquivas o no los tubos
            this.pipes.forEach(pipe => {
                if (pipe.x < 50 && pipe.x > 0) this.score++ //ganas puntos
                if (this.checkCollision(pipe)) this.resetGame() //o pierdes
            })

            // esto evita que te salgas por arriba o abajo del lienzo del juego
            if (this.birdY > 770 || this.birdY < 0) {
                this.resetGame()
            }
        },
        checkCollision(pipe) {
            // las colisiones estan hardcodeadas con valores manualmente puestos segun la resolucion del juego
            // lo se, se ve horrible
            const birdLeft = 55
            const birdRight = 75
            const pipeLeft = pipe.x
            const pipeRight = pipe.x + 50

            //esto se podria decir que es como la hitbox del disque pajaro o la bola
            const birdTop = this.birdY + 5
            const birdBottom = this.birdY + 25
            const gapTop = pipe.gapY - 80
            const gapBottom = pipe.gapY + 80
            //en vez de checar si colisiona con los tubos mejor checamos si pasa por el agujero

            const isInPipeX = birdRight > pipeLeft && birdLeft < pipeRight
            const isOutsideGapY = birdTop < gapTop || birdBottom > gapBottom

            return isInPipeX && isOutsideGapY
        },
        resetGame() {
            this.isStarted = false
            this.birdY = 200
            this.velocity = 0
            this.pipes = []
            this.score = 0
            //simplemente reinicia todo y vuelve la estado de click para iniciar
        }
    },
    mounted() {
        this.gameInterval = setInterval(this.updateGame, 30)
    },
    beforeDestroy() {
        clearInterval(this.gameInterval)
    }
}
</script>

<style scoped>
    .game {
        width: 600px;
        height: 800px;
        background: skyblue;
        position: relative;
        overflow: hidden;
        cursor: pointer;
    }
    .score {
        position: absolute;
        top: 10px;
        left: 10px;
        font-size: 20px;
        font-weight: bold;
    }
    .start-text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 24px;
        font-weight: bold;
        background: rgba(255, 255, 255, 0.8);
        padding: 10px 20px;
        border-radius: 10px;
        text-align: center;
    }
</style>