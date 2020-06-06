<template>
    <div id="app">
        <!--  tot hier  Afblijven -->
        <div class="topmargin">
            <h1 id="title">TRIPPIN'⛱</h1>
            <div class="step">
                <h2> Wat is je inkomen per maand?</h2>
                <input type="text" v-model="income"/> <span> €/maand</span>
                <h2> Wat zijn je gemiddelde uitgaven per maand?</h2>
                <input type="text" v-model="expensesWork"/> <span> €/maand</span>
                <div>
                    <button type="button" >Submit</button>
                </div>
            </div>

            <div class="step">
                <h2>Hoeveel wil je op reis per dag te besteden hebben?</h2>
                <input type="text" v-model="expensesTrip"/><span>€/dag</span>
                <h2>Hoelang wil je op reis?</h2>
                <input type="text" v-model="timeTrip"/><span>maanden</span>
                <div>
                    <button type="button" @click="calculate">Submit</button>
                </div>
            </div>

            <div class="step">
                <p>Je Trippin' Factor is...
                    <span v-text="trippinfactor"></span>
                </p>

                <p>
                    Dit betekent dat je
                </p>

<!--                <Plotly :data="data" :layout="layout" :display-mode-bar="false"></Plotly>-->
                <span v-text="totalWork"></span>
                <p>maanden moet werken...</p>
            </div>
        </div>
    </div>
</template>

<script>
    import { Plotly } from 'vue-plotly';

    export default {
        components: {
            Plotly
        },
        data() {
            return {
                income: 2000,
                expensesWork: 1800,
                expensesTrip: 50,
                timeTrip: null,
                trippinfactor: null,
                timeWork: null,
                totalWork:null,
                data: null,
                layout:null,
            }
        },
        methods: {
            calculate() {
                let gross = (this.expensesTrip*30.5)/(this.income - this.expensesWork);
                this.trippinfactor=gross.toFixed(2);
                console.log(gross);
                let work = (this.trippinfactor)*this.timeTrip;
                this.timeWork=work.toFixed(2);
                let totalWork = work*gross;
                this.totalWork=totalWork.toFixed(2);


                // this.data = [{
                //     values: [this.timeTrip, totalWork],
                //     labels: ['Maanden op Reis', 'Maanden aan de Arbeid'],
                //     type: 'pie'
                // }];
                //
                // this.layout = {
                //     height: 200,
                //     width: 400,
                //
                // };
                // this.options = {
                //     backgroundColor: 'transparent',
                // }

            }
        }
    }
</script>
<style src="./assets/style.css"></style>
<style>
    body {
        font-family: Calibri;
        background-color: #96abe5;
    }
    #title {
        font-size: 145px;
        text-align: center;
    }
    .step {
        background-color: midnightblue;
        color: white;
        padding: 10px;
        display: inline-block;
        width: 31%;
        margin: 5px;
        height: 200px;
        vertical-align: middle;
        position: relative;


    }
    .step input {
        width: 50px;
        padding: 3px;
    }
    .step h2 {
        margin-bottom: 5px;
        margin-top: 5px;
    }
    .step button{
        position: absolute;
        right: 10px;
        bottom: 10px;
    }
    .topmargin{
        margin-top: 70px;
        margin-left: 20px;
        margin-right: 20px;
    }

</style>
