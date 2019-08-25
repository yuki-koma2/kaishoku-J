<template>
    <section class="calculation Calc">
        <h1>calc</h1>

            <div v-if="errors.length">
                <p>Please correct the following error(s):</p>
                <ul>
                    <li v-for="error in errors" :key="error">{{ error }}</li>
                </ul>
            </div>
            <div class="member" v-for="player in players" :key="player.id">
                <p>
                    <label v-bind:for="'playerVal' + player.id">{{player.name}}</label>
                    <input
                            v-bind:id="'playerVal' + player.id"
                            v-model="player.value"
                            type="number"
                            v-bind:name="'playerVal' + player.id"
                    >
                </p>

            </div>
            <p>
                <label for="realVal">real value</label>
                <input
                        id="realVal"
                        v-model="realValue"
                        type="number"
                        name="realVal"
                >
            </p>

            <input
                    type="button"
                    value="Submit"
                    id="calc--submit"
                    v-on:click="checkInputDataCalc"
            >

        <div class="result" v-if="this.isCalced">
            ok
        </div>
    </section>
</template>

<script>
    // Tsで書くことを想定して、コードを書きます。今はTsの書き方あまりわからない…
    export default {
        name: "Calc",
        data() {
            return {
                players: [
                    {
                        id: 1,
                        name: 'yuri',
                        value: 0,
                        diff: 0,
                        rank: 0,
                    },
                    {
                        id: 2,
                        name: 'まゆねえ',
                        value: 0,
                        diff: 0,
                        rank: 0,
                    },
                    {
                        id: 3,
                        name: 'kinsho',
                        value: 0,
                        diff: 0,
                        rank: 0,
                    },
                    {
                        id: 4,
                        name: 'ますらお',
                        value: 0,
                        diff: 0,
                        rank: 0,
                    },
                    {
                        id: 5,
                        name: '星野',
                        value: 0,
                        diff: 0,
                        rank: 0,
                    },
                ],
                playerData:
                    {
                        id: 0,
                        name: "",
                        value: 0,
                        diff: 0,
                        rank: 0,
                    },
                members: [
                    'yuri',
                    'まゆねえ',
                    'kinsho',
                    'ますらお',
                    '星野',
                    'koma',
                ],
                errors: [],
                realValue: 0,
                isCalced:false,
            }
        },
        methods: {
            checkInputDataCalc: function () {
                console.log("ok");
                this.calcAll();
            },
            calcAll: function () {
                this.players.forEach(player => {
                        player.diff = player.value - this.realValue;
                        console.log(player);
                    }
                );
                this.createRank();
                this.isCalced = true;
            },
            createRank: function () {
                this.players.sort((a, b) => {
                    if (a.diff < b.diff) return -1;
                    if (a.diff > b.diff) return 1;
                    return 0;
                });
                console.table(this.players);
                this.players.forEach((player,index) => {
                    console.log(index);
                    player.rank = index + 1;
                    console.log(player);
                })
            },
        },
    };
</script>

<style scoped>

</style>
