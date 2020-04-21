<template>
    <div class="overlay" v-show="show">
        <p class="message">{{contents}}</p>
        <button class="play-again" @click="restart">再玩一次</button>
    </div>
</template>

<script>

    export default {
        data () {
            return {}
        },
        props: {
            game: {
                type: Object,
                required: true
            },
            onRestart: {
                type: Function,
                required: true
            }
        },
        computed: {
            show () {
                return this.game.hasWon() || this.game.hasLost()
            },
            contents () {
                if (this.game.hasWon()) {
                    return '2048 完成！'
                } else if (this.game.hasLost()) {
                    return '游戏结束'
                } else {
                    return ''
                }
            }
        },

        methods: {
            restart () {
                this.onRestart && this.onRestart()
            }
        },
        components: {}
    }
</script>
