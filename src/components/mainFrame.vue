<template>
  <div v-show="isShow2">
    <h1 id="mainTitle">⛱&#xFE0E; Trivia Quiz</h1>
    <label for="pretraga">🔍&#xFE0E; Pretraga:</label>
    <input type="text" id="pretraga" name="pretraga" /><br /><br />
    <button v-on:click="searchQuestion()" class="btn-orange">
      🔍&#xFE0E; Pretraži pitanje</button
    ><br /><br />
    <div
      style="
        width: 100%;
        height: 500px;
        overflow-y: auto;
        border: 1px solid black;
      "
    >
      <table style="width: 100%" id="t1">
        <tr>
          <th>Pitanje</th>
          <th>Odgovor A</th>
          <th>Odgovor B</th>
          <th>Odgovor C</th>
          <th>Točan odgovor</th>
        </tr>
        <tr v-for="i in alist" :key="i.BrojPitanja">
          <td>{{ i.Pitanje }}</td>
          <td>{{ i.OdgovorA }}</td>
          <td>{{ i.OdgovorB }}</td>
          <td>{{ i.OdgovorC }}</td>
          <td>{{ i.TocanOdgovor }}</td>
        </tr>
      </table>
    </div>
    <button id="gameBtn" class="btn-orange" v-on:click="openGF()">
      Započni igru
    </button>
  </div>
</template>

<script>
//import axios from "axios";
//var activeNumber = 0;
//var lovac = 0;
//var igrac = 2;
/*const HTTP = axios.create({
  baseURL: "https://localhost:44365/",
  headers: {},
});*/
export default {
  name: "mainFrame",
  data() {
    return {
      alist: [
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
      blist: [],
      isShow2: true,
    };
  },
  mounted() {
    this.$root.$on("closeGF", () => {
      this.isShow2 = true;
    });
    /*HTTP.get("api/get_all")
      .then((response) => {
        this.alist = response.data;
      })
      .catch((e) => {
        console.log(e);
      });*/
  },
  methods: {
    /*getSpecific(BP) {
      HTTP.get("api/get_specific/" + BP)
        .then((response) => {
          this.blist = response.data;
          document.getElementById("tp").innerHTML =
            "Trenutno pitanje: " + this.blist.Pitanje;
          document.getElementById("oa").innerHTML =
            "Odgovor A: " + this.blist.OdgovorA;
          document.getElementById("ob").innerHTML =
            "Odgovor B: " + this.blist.OdgovorB;
          document.getElementById("oc").innerHTML =
            "Odgovor C: " + this.blist.OdgovorC;
          document.getElementById("to").innerHTML =
            "Točan odgovor: " + this.blist.TocanOdgovor;
          activeNumber = this.blist.BrojPitanja;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    addQuestion() {
      if (
        document.getElementById("pitanje").value != "" &&
        document.getElementById("odgovorA").value != "" &&
        document.getElementById("odgovorB").value != "" &&
        document.getElementById("odgovorC").value != "" &&
        (document.getElementById("A").checked != false ||
          document.getElementById("B").checked != false ||
          document.getElementById("C").checked != false)
      ) {
        var selected = "";
        var radios = document.getElementsByName("rbtn");
        for (var radio of radios) {
          if (radio.checked) {
            selected = radio.value;
          }
        }
        HTTP.post("api/add_q", {
          Pitanje: document.getElementById("pitanje").value,
          OdgovorA: document.getElementById("odgovorA").value,
          OdgovorB: document.getElementById("odgovorB").value,
          OdgovorC: document.getElementById("odgovorC").value,
          TocanOdgovor: selected,
        });
      } else {
        alert("Jedno ili više polja je prazno");
      }
    },
    updateQuestion() {
      if (
        document.getElementById("Apitanje").value != "" &&
        document.getElementById("AodgovorA").value != "" &&
        document.getElementById("AodgovorB").value != "" &&
        document.getElementById("AodgovorC").value != "" &&
        (document.getElementById("AA").checked != false ||
          document.getElementById("AB").checked != false ||
          document.getElementById("AC").checked != false)
      ) {
        var selected = "";
        var radios = document.getElementsByName("Arbtn");
        for (var radio of radios) {
          if (radio.checked) {
            selected = radio.value;
          }
        }
        HTTP.put("api/update_q", {
          BrojPitanja: activeNumber,
          Pitanje: document.getElementById("Apitanje").value,
          OdgovorA: document.getElementById("AodgovorA").value,
          OdgovorB: document.getElementById("AodgovorB").value,
          OdgovorC: document.getElementById("AodgovorC").value,
          TocanOdgovor: selected,
        });
      } else {
        alert("Jedno ili više polja je prazno");
      }
    },
    deleteQuestion() {
      HTTP.delete("api/delete_q", {
        headers: {
          "Content-Type": "application/json",
        },
        data: {
          BrojPitanja: activeNumber,
        },
      });
    },*/
    searchQuestion() {
      var input, filter, table, tr, td, i, txtValue;
      input = document.getElementById("pretraga");
      filter = input.value;
      table = document.getElementById("t1");
      tr = table.getElementsByTagName("tr");
      for (i = 0; i < tr.length; i++) {
        td = tr[i].getElementsByTagName("td")[0];
        if (td) {
          txtValue = td.textContent || td.innerText;
          if (txtValue.indexOf(filter) > -1) {
            tr[i].style.display = "";
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    },
    openGF() {
      this.$root.$emit("openGF");
      this.isShow2 = false;
    },
  },
};
</script>
<style>
body {
  background: black;
  background-image: linear-gradient(to right, #434343 0%, black 100%);
  scroll-behavior: smooth;
}
h1,
h2,
h3,
h4,
h5,
h6,
label,
table {
  color: white;
}
table {
  border: 1px solid orange;
}
#gameBtn {
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
#mainTitle {
  animation: flow 2s ease-in-out infinite;
  background: linear-gradient(to right, #c6ffdd, #fbd786, #f7797d);
  background-size: 200%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
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
input {
  color: white;
  border-width: 1px;
  border-radius: 7px;
  background: #e96443;
  background: -webkit-linear-gradient(to right, #904e95, #e96443);
  background: linear-gradient(to right, #904e95, #e96443);
}
.currentQ {
  position: fixed;
  top: 5px;
  left: 5px;
  text-align: center;
  background: black;
  background-image: linear-gradient(to left, #434343 0%, black 100%);
  border: 1px solid orange;
  padding: 10px;
  border-radius: 10px;
  max-width: 30%;
}
</style>