<template>
    <div class="container-fluid">
        <!-- Page Heading -->
        <!--<div class="d-sm-flex align-items-center justify-content-between mb-4">
            <h1 class="h3 mb-0 text-gray-800">Dashboard</h1>
            <button type="button" class="btn btn-info" @click="getAllValues">
                Get All Entries
            </button>
            <button type="button" class="btn btn-info" @click="getAllMonthsByYear">
                Get All Months
            </button>
            <button
                type="button"
                class="btn btn-info"
                @click="getAllDaysByMonthAndYear"
            >
                Get All Days
            </button>
            <button type="button" class="btn btn-info" @click="createValues">
                Create New Values
            </button>
            <button type="button" class="btn btn-info" @click="getDataByDay">
                Get Data by Day
            </button>
            <button type="button" class="btn btn-info" @click="getDataByMonth">
                Get Data by Month
            </button>
            <button type="button" class="btn btn-info" @click="getDataByYear">
                Get Data by Year
            </button>
        </div>-->
        <!-- Content Row -->
        <div class="row">
            <!-- Pending Requests Card Example -->
            <div class="col">
                <div class="card" style="width: 20rem">
                    <div class="card-header">
                        <strong>Baterry Voltage</strong>
                    </div>
                    <div class="card-body">
                        <div>
                            <img
                                src="/baterry.png"
                                alt="Battery"
                                class="rounded-circle"
                                height="200px"
                                widht="180px"
                            />
                        </div>
                        <br/>
                        <p class="card-text">{{ values.battery_voltage }} V</p>
                    </div>
                    <div class="card-footer text-muted">
                        <div>
                            <p>State</p>
                        </div>
                        <div>
                            <div class="row">
                                <div v-show="values.battery_voltage" class="col">
                                    <button type="button" class="btn btn-success">
                                        Connected
                                    </button>
                                </div>
                                <div v-show="!values.battery_voltage" class="col">
                                    <button type="button" class="btn btn-danger">
                                        Disconnected
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col">
                <div class="card" style="width: 20rem">
                    <div class="card-header">
                        <strong>Solar Panel Voltage</strong>
                    </div>
                    <div class="card-body">
                        <div>
                            <img
                                src="/solarpanel.png"
                                alt="Solar Panel"
                                class="rounded-circle"
                                height="200px"
                                widht="180px"
                            />
                        </div>
                        <br/>
                        <p class="card-text">{{ values.solar_panel_voltage }} V</p>
                    </div>
                    <div class="card-footer text-muted">
                        <div>
                            <p>State</p>
                        </div>
                        <div>
                            <div class="row">
                                <div v-show="values.solar_panel_voltage" class="col">
                                    <button type="button" class="btn btn-success">
                                        Connected
                                    </button>
                                </div>
                                <div v-show="!values.solar_panel_voltage" class="col">
                                    <button type="button" class="btn btn-danger">
                                        Disconnected
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col">
                <div class="card" style="width: 20rem">
                    <div class="card-header">
                        <strong>Consumption Current</strong>
                    </div>
                    <div class="card-body">
                        <div>
                            <img
                                src="/currentconsumption.png"
                                alt="Consumption Current"
                                class="rounded-circle"
                                height="200px"
                                widht="180px"
                            />
                        </div>
                        <br/>
                        <p class="card-text">{{ values.consumption_current }} A</p>
                    </div>
                    <div class="card-footer text-muted">
                        <div>
                            <p>State</p>
                        </div>
                        <div>
                            <div class="row">
                                <div v-show="values.consumption_current" class="col">
                                    <button type="button" class="btn btn-success">
                                        Consuming
                                    </button>
                                </div>
                                <div v-show="!values.consumption_current" class="col">
                                    <button type="button" class="btn btn-danger">
                                        Not consuming
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col">
                <div class="card" style="width: 20rem">
                    <div class="card-header">
                        <strong>Produciong Current</strong>
                    </div>
                    <div class="card-body">
                        <div>
                            <img
                                src="/produciongCurrent.png"
                                alt="Consumption Current"
                                class="rounded-circle"
                                height="200px"
                                widht="180px"
                            />
                        </div>
                        <br/>
                        <p class="card-text">{{ values.producing_current }} A</p>
                    </div>
                    <div class="card-footer text-muted">
                        <div>
                            <p>State</p>
                        </div>
                        <div>
                            <div class="row">
                                <div v-show="values.producing_current" class="col">
                                    <button type="button" class="btn btn-success">
                                        Producing
                                    </button>
                                </div>
                                <div v-show="!values.producing_current" class="col">
                                    <button type="button" class="btn btn-danger">
                                        Not producing
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-md-3" style="padding-right: 5%">
                <br/>
                <br/>
                <label class="h3 mr-3 text-gray-800">Show statistics</label>

                <select v-model="opcao" @change="chartChanged($event)">
                    <option disabled value=" ">Select a option</option>
                    <option value="dia">For day</option>
                    <option value="mes">For month</option>
                    <option value="ano">For year</option>
                </select>
            </div>
            <div class="col-md-9"></div>
        </div>
        <div class="row">
            <div class="col-sm-2">
                <br/>
                <br/>
                <label class="h3 mr-3 text-gray-800">Year</label>
                <select
                    v-show="anos"
                    v-model="data.ano"
                    @change="dateChanged('ano')"
                    style="
            background: transparent;
            padding-left: 10px;
            border: 1px solid black;
          "
                >
                    <option v-for="ano in anos" :value="ano" :key="ano">
                        {{ ano }}
                    </option>
                </select>
                <div v-show="!anos" class="alert alert-primary" role="alert">
                    Loading...
                </div>
            </div>
            <div class="col-sm-2">
                <br/>
                <br/>
                <div v-show="opcao == 'dia' || opcao == 'mes'">
                    <label class="h3 mr-3 text-gray-800">Month</label>
                    <select
                        v-show="meses"
                        v-model="data.mes"
                        @change="dateChanged('mes')"
                        style="
              background: transparent;
              padding-left: 10px;
              border: 1px solid black;
            "
                    >
                        <option v-for="mes in meses" :value="mes" :key="mes">
                            {{ mes }}
                        </option>
                    </select>
                    <div v-show="!meses" class="alert alert-primary" role="alert">
                        Select an year
                    </div>
                </div>
            </div>
            <div class="col-sm-2">
                <br/>
                <br/>
                <div v-show="opcao == 'dia'">
                    <label class="h3 mr-3 text-gray-800">Day</label>
                    <select
                        v-show="dias"
                        v-model="data.dia"
                        style="
              background: transparent;
              padding-left: 10px;
              border: 1px solid black;
            "
                    >
                        <option v-for="dia in dias" :value="dia" :key="dia">
                            {{ dia }}
                        </option>
                    </select>
                    <div v-show="!dias" class="alert alert-primary" role="alert">
                        Select a month
                    </div>
                </div>
            </div>
            <div class="col-sm-6"></div>
        </div>
        <div
            class="row"
            v-show="
        (opcao == 'dia' && data.dia) ||
        (opcao == 'mes' && data.mes) ||
        (opcao == 'ano' && data.ano)
      "
        >
            <div class="col-md-2">
                <button class="btn btn-info" @click="getData">Get data</button>
            </div>
            <div class="col-md-10"></div>
        </div>
        <div v-show="loading" class="row">
            <div class="col-md-12">
                <div  class="alert alert-primary" role="alert">
                    Loading...
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <LineChart @chart-rendered="chartRendered" :key="rerender" :data="dados" :labels="labels"/>
            </div>
        </div>
    </div>
</template>

<script>
    import LineChart from "./LineChart.vue";

    const axios = require("axios").default;

    export default {
        name: "dashboard",
        components: {
            LineChart,
        },
        data: function () {
            return {
                rerender: 1,
                values: {},
                dados: {
                    consumed: [],
                    produced: [],
                },
                labels: [],
                labelsDef: {
                    dia: [
                        "00:00",
                        "01:00",
                        "02:00",
                        "03:00",
                        "04:00",
                        "05:00",
                        "06:00",
                        "07:00",
                        "08:00",
                        "09:00",
                        "10:00",
                        "11:00",
                        "12:00",
                        "13:00",
                        "14:00",
                        "15:00",
                        "16:00",
                        "17:00",
                        "18:00",
                        "19:00",
                        "20:00",
                        "21:00",
                        "22:00",
                        "23:00",
                    ],
                    mes: [
                        "01",
                        "02",
                        "03",
                        "04",
                        "05",
                        "06",
                        "07",
                        "08",
                        "09",
                        "10",
                        "11",
                        12,
                        13,
                        14,
                        15,
                        16,
                        17,
                        18,
                        19,
                        20,
                        21,
                        22,
                        23,
                        24,
                        25,
                        26,
                        27,
                        28,
                        29,
                        30,
                        31,
                    ],
                    ano: [
                        "Jan",
                        "Feb",
                        "Mar",
                        "Apr",
                        "May",
                        "Jun",
                        "Jul",
                        "Aug",
                        "Set",
                        "Oct",
                        "Nov",
                        "Dec",
                    ],
                },
                data: {
                    dia: null,
                    mes: null,
                    ano: null,
                },
                opcao: "dia",
                dias: null,
                meses: null,
                anos: null,
                dateString: null,
                loading: false,
            };
        },
        methods: {
            getValues: function () {
                axios
                    .get("http://"+window.location.host.split(":")[0]+":8080/payload")
                    .then((response) => {
                        //console.log("LAST VALUE");
                        //console.log(response);
                        this.values = response.data;

                        this.getAllYears();
                    })
                    .catch((err) => {
                        //console.log(err);
                    });
            },
            getAllValues: function () {
                axios.get("http://"+window.location.host.split(":")[0]+":8080/payload/all").then((response) => {
                    console.log("ALL ENTRIES");
                    //this.values = response.data;
                    // console.log(response);
                });
            },
            getDataByDay: function () {
                axios
                    .get(
                        "http://"+window.location.host.split(":")[0]+":8080/values/hours/" +
                        "31" +
                        "/" +
                        "05" +
                        "/" +
                        "2021"
                    )
                    .then((response) => {
                        // console.log("DATA OF DAY [HOURS]");
                        // console.log(response);
                        //this.dados.consumed = response.data.consumed;
                        //this.dados.produced = response.data.produced;
                        //console.log(this.dados);
                    });
            },
            getDataByMonth: function () {
                axios
                    .get("http://"+window.location.host.split(":")[0]+":8080/values/days/" + "05" + "/" + "2021")
                    .then((response) => {
                        // console.log("DATA OF MONTH [DAYS]");
                        // console.log(response);
                        //this.dados.consumed = response.data.consumed;
                        //this.dados.produced = response.data.produced;
                        //console.log(this.dados);
                    });
            },
            getDataByYear: function () {
                axios
                    .get("http://"+window.location.host.split(":")[0]+":8080/values/months/" + "2021")
                    .then((response) => {
                        // console.log("DATA OF YEAR [MONTHS]");
                        // console.log(response);
                        //this.dados.consumed = response.data.consumed;
                        //this.dados.produced = response.data.produced;
                        //console.log(this.dados);
                    });
            },
            getAllDaysByMonthAndYear: function (month, year) {
                // console.log("Entrou");
                axios
                    .get("http://"+window.location.host.split(":")[0]+":8080/days/" + month + "/" + year)
                    .then((response) => {
                        // console.log("MESES");
                        //console.log(response);
                        this.dias = response.data;
                    });
            },
            getAllMonthsByYear: function (year) {
                console.log("Entrou 1 ");
                axios.get("http://"+window.location.host.split(":")[0]+":8080/months/" + year).then((response) => {
                    console.log("Ano");
                    //console.log(response);
                    this.meses = response.data;
                    //console.log(this.meses);
                });
            },
            getAllYears: function () {
                axios.get("http://"+window.location.host.split(":")[0]+":8080/years").then((response) => {
                    //console.log("ANOS");
                    //console.log(response);
                    this.anos = response.data;
                    //console.log(this.anos);
                });
            },
            createValues: function () {
                //Este é o objeto que guarda na base de dados, é objeto enviado pelo ESP + os dados que acrescenta
                //o RASP, e que depois o back põe dentro da bd.
                let body = {
                    battery_voltage: 13,
                    solar_panel_voltage: 13,
                    consumption_current: 0.23,
                    producing_current: 0.43,
                    full_date: "2021-05-31 2:58:43",
                    date: {
                        year: "2021",
                        day: "31",
                        month: "05",
                        hour: "02",
                        minute: "58",
                        second: "43",
                    },
                };
                axios.post("http://"+window.location.host.split(":")[0]+":8080/payload", body).then((response) => {
                    //console.log("NEW ENTRY");
                    //console.log(response);
                });
            },
            chartChanged(event) {
                this.labels = this.labelsDef[event.target.value];
                this.dados.consumed = [];
                this.dados.produced = [];
                this.data.ano = null;
                this.data.mes = null;
                this.data.dia = null;
            },
            dateChanged(section) {
                switch (section) {
                    case "mes":
                        this.data.dia = null;
                        this.getAllDaysByMonthAndYear(this.data.mes, this.data.ano);
                        break;
                    case "ano":
                        this.data.mes = null;
                        this.data.dia = null;
                        this.getAllMonthsByYear(this.data.ano);
                }
            },
            chartRendered(){
                this.loading=false;
            },
            getData() {

                this.loading = true;
                this.dados.produced = [];
                this.dados.consumed = [];

                let url;

                if (this.data.dia) {
                    url =
                        "http://"+window.location.host.split(":")[0]+":8080/values/hours/" +
                        this.data.dia +
                        "/" +
                        this.data.mes +
                        "/" +
                        this.data.ano;
                } else if (this.data.mes) {
                    url =
                        "http://"+window.location.host.split(":")[0]+":8080/values/days/" +
                        this.data.mes +
                        "/" +
                        this.data.ano;
                } else {
                    url = "http://"+window.location.host.split(":")[0]+":8080/values/months/" + this.data.ano;
                }

                axios.get(url).then((response) => {
                    // console.log(response.data);

                    response.data.forEach((item) => {
                        this.dados.consumed.push(item.consumed*12.0);
                        this.dados.produced.push(item.produced*12.0);

                    });
                    this.rerender = !this.rerender;

                });
            },
        },
        mounted() {
            console.log(window.location.pathname)
            this.labels = this.labelsDef.dia;
            this.getValues();
        },
    };
</script>

<style>
    #app {
        font-family: "Avenir", Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
