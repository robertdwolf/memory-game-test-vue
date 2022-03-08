<template>
    <div class="card">
        <div
            class="card-inner"
            :class="flipped.includes(index) || matched.includes(index) || !started ? 'active' : ''"
        >
            <div class="card-front"></div>
            <div class="card-back" :style="{backgroundImage:`url(${image})`}"></div>
        </div>        
    </div>
</template>

<script>

export default {
    name: 'Card',
    props: ['image','name','index','started','flipped','matched'],
    data() {
        return {}
    },
}
</script>

<style lang='scss'>
@import './src/main.scss';

.card {
    display: block;
    width: calc(12.5%);
    margin: 10px 0 0;
    padding: 0 5px;
    perspective: 1400px;
    transform: translate3d(0,0,0);
    @include breakpoint('tabletPortrait') {
        width: calc(20%);
    }
    @include breakpoint('mobile') {
        width: calc(25%);
    }
}

.card-inner {
    height: 0;
    padding-bottom: 100%;
    position: relative;
    transform: rotateY(0deg);
    transform-style: preserve-3d;
    transition: transform .3s;
    cursor: pointer;
    &.active {
        transform: rotateY(180deg);
        pointer-events: none;
    }
}

.card-front,
.card-back {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    box-shadow: 0 2px 5px 0px rgba(0,0,0,.4);
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

.card-front {
    background: $color_blue url('/static/images/card-front.png') no-repeat 50% 50%/cover;
    z-index: 1;
}

.card-back {
    background: no-repeat 50% 50%/100% 100%;
    transform: rotateY(180deg);
}
</style>