<template>
    <div class="stats">
        <div class="stats-left">
            <button v-if="!started" @click="$emit('update:started', true)">Start Game</button>
            <button v-if="started" @click="$emit('update:started', false)">Restart Game</button>
        </div>
        <div class="stats-right">
            <div class="moves">Moves <span>{{ moves }}</span></div>
        </div>
    </div>
    <div class="modal" v-if="gameWon">You Won!</div>
</template>

<script>

export default {
    name: 'Stats',
    props: ['flipped','started','moves','gameWon'],
    methods: {
        startGame() {
            flipped = []
        }
    },
    data() {
        return {}
    },
}
</script>

<style lang='scss'>
@import './src/main.scss';

.stats {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 60px;
    background: $color_blue;
    padding: 15px;
}

.stats-left {
    display: flex;
    padding: 0 15px 0 0;
    button {
        margin: 0 15px 0 0;
    }
}

stats-right {
    display: flex;
    padding: 0 0 0 15px;
}

button {
    display: table;
    width: auto;
    height: calc(60px - 30px);
    margin: 0;
    padding: 2px 10px 0;
    background: $color_white;
    border: 0;
    border-radius: 6px;
    font-family: 'Montserrat', sans-serif;
    font-size: 14px;
    line-height: 1.4;
    font-weight: 700;
    text-transform: uppercase;
    color: $color_blue;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
}

.moves {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    font-size: 14px;
    line-height: 1.4;
    font-weight: 700;
    text-transform: uppercase;
    color: $color_white;
    span {
        display: inline-block;
        width: 36px;
        height: 36px;
        margin: 0 0 0 5px;
        padding: 9px 5px 5px;
        background: $color_white;
        border-radius: 100em;
        color: $color_blue;
        text-align: center;
    }
}

.modal {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 200px;
    position: fixed;
    top: 50%;
    left: 50%;
    z-index: 100;
    transform: translate(-50%,-50%);
    padding: 15px;
    background: $color_blue;
    font-family: 'Montserrat', sans-serif;
    font-size: 30px;
    line-height: 1.4;
    font-weight: 700;
    text-transform: uppercase;
    color: $color_white;
    text-align: center;
}
</style>