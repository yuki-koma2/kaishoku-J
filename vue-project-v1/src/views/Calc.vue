<template>
    <section class="calculation">
        <h1>calc</h1>
        <form
                id="calc-form"
        >
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
                    v-on:click="this.checkInputDataCalc()"
            >
        </form>
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
            }
        },
        created: function () {
            // let i = 0;
            console.log("created");
            // while (i < 5){
            // console.log(i);
            //     this.playerData.name = this.members[i];
            //     console.log(this.members[i]);
            //     console.log(this.playerData.name);
            //     this.playerData.id = i;
            //     console.log(this.playerData);
            //     this.players.push(Object.create(this.playerData));
            //     console.log(this.players);
            //     i++;
            // }
        },
        method: {
            checkInputDataCalc: function (e) {
                e.preventDefault();
                this.calcAll();
                // console.trace(this.calcAll());
            },
            calcAll: function () {
                this.players.forEach(player => {
                        player.diff = player.value - this.realValue;
                        console.log(player);
                    }
                );
                this.createRank();
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
                    player.rank = index;
                    console.log(player);
                })
            },
        },
    };
</script>

<style scoped>

</style>
