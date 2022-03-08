<template>
    <Stats
        v-model:started="started"
        v-model:gameWon="gameWon"
        :started="started"
        :moves="moves"
    />
    <div class="card-container">
        <Card
            v-for="(card, index) of dupCards"
            :key="index"
            :name="card.name"
            :image="card.image"
            :index="index"
            :started="started"
            :flipped="flipped"
            :matched="matched"
            @click="flipCard(card.name, index)"
        >
        </Card>
    </div>
</template>

<script>
import Card from './components/Card.vue'
import Stats from './components/Stats.vue'

export default {
    name: 'App',
    props: ['image','name'],
    components: {
        Card, Stats,
    },
    methods: {
        flipCard(name, index) {
            if (!this.started) return

            this.flipped.push(index)

            this.moves = this.moves+1

            setTimeout(()=>{
                // Check if clicked second time
                if (this.prevName.name) {
                    // Check if match
                    if (this.prevName.name === name) {
                        this.prevName.name = ''
                        this.matched.push(...this.flipped)
                        this.flipped = []

                        // Check if all cards matched
                        if (this.matched.length === this.dupCards.length) {
                            this.gameWon = true
                        }

                    } else {
                        setTimeout(()=>{
                            this.prevName.name = ''
                            this.flipped = []
                        }, 300)
                    }
                } else {
                    this.prevName = {name:name, index:index}
                }
            }, 300)
        }
    },
    watch: {
        started(value, oldValue) {
            // Check if game is started
            if (value) {
            } else {
                this.flipped = []
                this.matched = []
                this.moves = 0
                this.gameWon = false
            }
        }
    },
    data() {
        return {
            cards: [
                {
                    name: 'Arizona',
                    image: require('/static/images/arizona.png'),
                },
                {
                    name: 'Auburn',
                    image: require('/static/images/auburn.png'),
                },
                {
                    name: 'Baylor',
                    image: require('/static/images/baylor.png'),
                },
                {
                    name: 'Connecticut',
                    image: require('/static/images/connecticut.png'),
                },
                {
                    name: 'Duke',
                    image: require('/static/images/duke.png'),
                },
                {
                    name: 'Florida',
                    image: require('/static/images/florida.png'),
                },
                {
                    name: 'Gonzaga',
                    image: require('/static/images/gonzaga.png'),
                },
                {
                    name: 'Kansas',
                    image: require('/static/images/kansas.png'),
                },
                {
                    name: 'North Carolina',
                    image: require('/static/images/north-carolina.png'),
                },
                {
                    name: 'Syracuse',
                    image: require('/static/images/syracuse.png'),
                },
                {
                    name: 'Villanova',
                    image: require('/static/images/villanova.png'),
                },
                {
                    name: 'Virginia',
                    image: require('/static/images/virginia.png'),
                },
            ],
            dupCards: '',
            prevName: {},
            flipped: [],
            matched: [],
            started: false,
            moves: 0,
            gameWon: false,
        }
    },
    created() {
        const shuffle = (array) => {
            let currentIndex = array.length,  randomIndex
            while (currentIndex != 0) {
                randomIndex = Math.floor(Math.random() * currentIndex)
                currentIndex--
                [array[currentIndex], array[randomIndex]] = [
                array[randomIndex], array[currentIndex]]
            }
            return array
        }

        this.dupCards = shuffle([...this.cards, ...this.cards])
    },
    mounted() {},
}
</script>

<style lang='scss'>
@import './src/main.scss';

@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700;900&display=swap');

/*================================================================================
CSS Reset
================================================================================*/

html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    vertical-align: baseline;
    font: inherit;
    font-size: 100%;
}

article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section, main {
    display: block;
}

body {
    line-height: 1;
}

ol, ul {
    list-style: none;
}

blockquote, q {
    quotes: none;
}

blockquote:before, blockquote:after, q:before, q:after {
    content: '';
    content: none;
}

table {
    border-spacing: 0;
    border-collapse: collapse;
}

:focus {
    outline: 0;
}

textarea {
    overflow: auto;
    resize: none;
}

html {
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
}

*, *:before, *:after {
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-tap-highlight-color: transparent;
}

/*================================================================================
Typography
================================================================================*/

/*
100 Thin (Hairline)
200 Extra Light (Ultra Light)
300 Light
400 Normal
500 Medium
600 Semi Bold (Demi Bold)
700 Bold
800 Extra Bold (Ultra Bold)
900 Black (Heavy)
*/

body {
    font-family: 'Montserrat', sans-serif;
    font-size: 16px;
    line-height: 1.4;
    font-weight: 400;
    color: $color_black;
}

p {
    margin: 0 0 15px;
    &:last-of-type {
        margin-bottom: 0;
        + {
            ul, ol {
                margin-top: 15px;
            }
        }
    }
}

ul {
    list-style: disc;
}

ol {
    list-style: decimal;
}

ul,
ol {
    margin: 0 0 15px 24px;
    &:last-of-type {
        margin-bottom: 0;
        + p {
            margin-top: 15px;
        }
    }
}

li {
    margin: 0 0 5px;
}

strong, b {
    font-weight: 700;
}

em, i {
    font-style: italic;
}

a {
    color: $color_blue;
    text-decoration: underline;
}

/*================================================================================
Structure
================================================================================*/

html,
body {
    background: $color_blue_light;
}

/*================================================================================
Components
================================================================================*/

.card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 0 5px 10px;
}
</style>