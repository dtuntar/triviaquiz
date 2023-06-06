<template>
  <div v-show="isShow">
    <h1 id="mainTitle2">🎮&#xFE0E; Igra</h1>
    <h1>{{ this.randlist[this.counter].Pitanje }}</h1>
    <button v-on:click="guess('A')" class="btn-orange">
      {{ this.randlist[this.counter].OdgovorA }}</button
    ><br /><br />
    <button v-on:click="guess('B')" class="btn-orange">
      {{ this.randlist[this.counter].OdgovorB }}</button
    ><br /><br />
    <button v-on:click="guess('C')" class="btn-orange">
      {{ this.randlist[this.counter].OdgovorC }}</button
    ><br /><br />
    <h1 id="ic" style="color: lightgreen">Igrač: 2</h1>
    <h1 id="lc" style="color: lightcoral">Lovac: 0</h1>
    <button id="gameBtn2" class="btn-orange" v-on:click="closeGF()">
      Glavni izbornik
    </button>
  </div>
</template>
<style>
.btn-orange {
  color: white;
  background: linear-gradient(
    180deg,
    #fff0e2,
    #fd7c05 8%,
    #744b2c 94%,
    #a94617
  );
  border-color: #fd7c05;
  border-radius: 10px;
  background-color: orange;
  font-size: 20px;
  margin-bottom: 5px;
  transition: 0.5s;
}
.btn-orange:hover,
.btn-orange:active,
.btn-orange:focus,
.btn-orange:visited {
  background: linear-gradient(
    180deg,
    #fff0e2,
    #5c2f06 8%,
    #994e0b 94%,
    #a94617
  );
  border-color: #422300;
  opacity: 0.7;
  cursor: pointer;
}
#gameBtn2 {
  position: fixed;
  top: 5px;
  right: 5px;
  width: 200px;
  height: 100px;
}
@keyframes flow {
  0% {
    background-position: 0 50%;
  }

  50% {
    background-position: 100% 50%;
  }

  100% {
    background-position: 0 50%;
  }
}
#mainTitle2 {
  animation: flow 2s ease-in-out infinite;
  background: linear-gradient(to right, #c6ffdd, #fbd786, #f7797d);
  background-size: 200%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
<script>
/*import axios from "axios";
const HTTP = axios.create({
  baseURL: "https://localhost:44365/",
  headers: {},
});*/
var lovac = 0;
var igrac = 2;
export default {
  data() {
    return {
      isShow: false,
      randlist: [
      {
          Pitanje: "Koliko iznosi jedna doza donirane krvi?",
          OdgovorA: "450 ml",
          OdgovorB: "600 ml",
          OdgovorC: "300 ml",
          TocanOdgovor: "A",
        },
        {
          Pitanje: "Koliko traje davanje krvi?",
          OdgovorA: "3-5 min",
          OdgovorB: "8-12 min",
          OdgovorC: "15-20 min",
          TocanOdgovor: "B",
        },
        {
          Pitanje: "Koliko traje davanje krvi posredstvom staničnog separatora?",
          OdgovorA: "10-20 min",
          OdgovorB: "20-30 min",
          OdgovorC: "30-90 min",
          TocanOdgovor: "C",
        },
        {
          Pitanje: "Može mi osoba davanjem krvi oboljeti od AIDS-a?",
          OdgovorA: "da",
          OdgovorB: "ne",
          OdgovorC: "ovisi o uzorku",
          TocanOdgovor: "B",
        },
        {
          Pitanje: "Koliko je litara krvi u ljudskom tijelu",
          OdgovorA: "5 l",
          OdgovorB: "5.2 l",
          OdgovorC: "4.8 l",
          TocanOdgovor: "A",
        },
        {
          Pitanje: "Koliko je krvnih grupa?",
          OdgovorA: "5",
          OdgovorB: "3",
          OdgovorC: "4",
          TocanOdgovor: "C",
        },
        {
          Pitanje: "Koliko života može spasiti jedna doza?",
          OdgovorA: "3",
          OdgovorB: "2",
          OdgovorC: "1",
          TocanOdgovor: "A",
        },
        {
          Pitanje: "Tko je otkrio krvne grupe?",
          OdgovorA: "Louis Pasteur",
          OdgovorB: "Karl Landsteiner",
          OdgovorC: "Alexander Flemming",
          TocanOdgovor: "B",
        },
        {
          Pitanje: "Koliko dana žive crvene krvne stanice?",
          OdgovorA: "90",
          OdgovorB: "150",
          OdgovorC: "120",
          TocanOdgovor: "C",
        },
        {
          Pitanje: "Koliki postotak obujma krvi čini plazma?",
          OdgovorA: "55%",
          OdgovorB: "40%",
          OdgovorC: "60%",
          TocanOdgovor: "A",
        },
        {
          Pitanje: "Koliko se dana mogu čuvati crvene krvne stanice?",
          OdgovorA: "120",
          OdgovorB: "42",
          OdgovorC: "112",
          TocanOdgovor: "B",
        },
        {
          Pitanje: "Koliko se testova izvodi nad svakoj dozi?",
          OdgovorA: "5",
          OdgovorB: "11",
          OdgovorC: "13",
          TocanOdgovor: "C",
        },
        {
          Pitanje: "Koliki postotak populacije ima krvnu grupu B?",
          OdgovorA: "10%",
          OdgovorB: "20%",
          OdgovorC: "30%",
          TocanOdgovor: "A",
        },
        {
          Pitanje: "Koliko se donacija provede svaki dan u svijetu?",
          OdgovorA: "130 000",
          OdgovorB: "38 000",
          OdgovorC: "540 000",
          TocanOdgovor: "B",
        },
        {
          Pitanje: "Koja je najtraženija grupa krvi?",
          OdgovorA: "A",
          OdgovorB: "B",
          OdgovorC: "O",
          TocanOdgovor: "C",
        },
      ],
      counter: 0,
    };
  },
  created() {
    this.$root.$on("openGF", () => {
      this.isShow = true;
    });
  },
  mounted() {
    /*HTTP.get("api/get_random").then((response) => {
      this.randlist = response.data;
    });*/
  },
  methods: {
    closeGF() {
      this.$root.$emit("closeGF");
      this.isShow = false;
      igrac = 2;
      lovac = 0;
      document.getElementById("ic").innerHTML = "Igrač: " + igrac;
      document.getElementById("lc").innerHTML = "Lovac: " + lovac;
      this.counter = 0;
      /*HTTP.get("api/get_random").then((response) => {
        this.randlist = response.data;
      });*/
    },
    guess(ans) {
      var lguess = Math.random();
      if (ans == this.randlist[this.counter].TocanOdgovor) {
        igrac++;
        this.counter++;
        document.getElementById("ic").innerHTML = "Igrač: " + igrac;
        if (igrac >= 10) {
          alert("Pobjeda!");
          igrac = 2;
          lovac = 0;
          document.getElementById("ic").innerHTML = "Igrač: " + igrac;
          document.getElementById("lc").innerHTML = "Lovac: " + lovac;
          this.counter = 0;
          /*HTTP.get("api/get_random").then((response) => {
            this.randlist = response.data;
          });*/
        } else if (lguess < 0.75 && igrac < 10) {
          lovac++;
          document.getElementById("lc").innerHTML = "Lovac: " + lovac;
        }
      } else {
        if (lguess < 0.75 && igrac != lovac) {
          lovac++;
          this.counter++;
          if (igrac == lovac) {
            alert("Gubitak!");
            igrac = 2;
            lovac = 0;
            document.getElementById("ic").innerHTML = "Igrač: " + igrac;
            document.getElementById("lc").innerHTML = "Lovac: " + lovac;
            this.counter = 0;
            /*HTTP.get("api/get_random").then((response) => {
              this.randlist = response.data;
            });*/
          }
          document.getElementById("lc").innerHTML = "Lovac: " + lovac;
        }
      }
    },
  },
};
</script>