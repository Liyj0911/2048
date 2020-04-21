<template>
    <div class="game" tabIndex="1">
        <div v-for="row_item in game.cells" :key="row_item.id">
            <TheCell v-for="col_item in row_item" :key="col_item.id"></TheCell>
        </div>
        <TheTile v-for="tile in tiles" :tile="tile" :key="tile.id"></TheTile>
        <GameEnd :game="game" :onRestart="onRestart"></GameEnd>
        得分{{game.score}}
    </div>
</template>

<script>
    import TheCell from './TheCell.vue'
    import TheTile from './TheTile.vue'
    import GameEnd from './GameEnd.vue'
    import Game from '../game'

    export default {
        data () {
            return {
                game: new Game()
            }
        },
        components: {
            TheCell,
            TheTile,
            GameEnd
        },
        mounted () {
            window.addEventListener('keydown', this.handleKeyDown.bind(this))
        },
        beforeDestroy () {
            window.removeEventListener('keydown', this.handleKeyDown.bind(this))
        },
        computed: {
            tiles () {
                return this.game.tiles
                    .filter(tile => tile.value !== 0)
            }
        },
        methods: {
            handleKeyDown (event) {
                if (this.game.hasWon()) {
                    return
                }
                if (event.keyCode >= 37 && event.keyCode <= 40) {
                    event.preventDefault()
                    var direction = event.keyCode - 37
                    this.game.move(direction)
                }
            },
            onRestart () {
                this.game = new Game()
            }
        }
    }
</script>
