<template>
  <div id="app">
    <div v-if="!perdu && !gagne">
      <div class="row">
        <div class="col-xs-4">
          <pre>Score: {{score}}</pre>
          <pre>Ratés : {{rates.length}}</pre>
        </div>
        <div class="col-xs-8">
                    <pre v-if="rates.length === 0">







          </pre>
          <pre v-if="rates.length === 1">






=======
          </pre>
          <pre v-if="rates.length === 2">

      |
      |
      |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 3">
  +===+
      |
      |
      |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 4">
  +===+
  |   |
      |
      |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 5">
  +===+
  |   |
  O   |
      |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 6">
  +===+
  |   |
  O   |
  |   |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 7">
  +===+
  |   |
  O   |
 /|   |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 8">
  +===+
  |   |
  O   |
 /|\  |
      |
      |
=======
          </pre>
          <pre v-if="rates.length === 9">
  +===+
  |   |
  O   |
 /|\  |
 /    |
      |
=======
          </pre>
          <pre v-if="rates.length === 10">
  +===+
  |   |
  O   |
 /|\  |
 / \  |
      |
=======
          </pre>
        </div>
      </div>

      <pre class="gros">
        <span v-for="l in motAAfficher">{{l}} </span>
      </pre>
      <div>
        <button class="btn btn-default" v-for="l in lettres" @click="clic(l)"
                :disabled="lettresChoisies.indexOf(l) > -1">{{l}}
        </button>
      </div>
    </div>
    <div v-if="perdu" class="danger">
      <pre>
  +===+
  |   |
  O   |
 /|\  |
 / \  |
      |
=======
          </pre>
      Vous avez perdu...<br>
      <button @click="reset" class="btn btn-danger">Recommencer</button>
    </div>
    <div v-if="gagne" class="success">
      Vous avez gagné...<br>
      <button @click="reset" class="btn btn-success">Recommencer</button>
    </div>

    &copy; m.tancoigne@gmail.com
  </div>
</template>

<script>

  const mots = ['serpent', 'chien', 'oiseau', 'cheval'];

  export default {
    name: 'app',
    data(){
      return {
        lettres: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'],
        score: 0,
        lettresChoisies: [],
        rates: [],
        reussis: [],
        mot: this.motAuHasard(),
        perdu: false,
        gagne: false,
      }
    },
    computed: {
      motAAfficher(){
        const mot = this.mot;
        let sortie = '';
        for (const l of mot) {
          sortie += this.reussis.indexOf(l) > -1 ? l : '_';
        }
        return sortie;
      }
    },
    methods: {
      clic(lettre){
        this.lettresChoisies.push(lettre);
        if (this.mot.indexOf(lettre) > -1) {
          this.reussis.push(lettre);
        } else {
          this.rates.push(lettre);
        }
        this.check();
      },
      check(){
        this.perdu = this.rates.length >= 10;
        this.gagne = this.motAAfficher === this.mot;
      },
      reset(){
        this.lettresChoisies = [];
        this.rates = [];
        this.reussis = [];
        this.mot = '';
        this.perdu = false;
        this.gagne = false;
        this.mot = this.motAuHasard();
      },
      motAuHasard(){
        return mots[Math.floor(Math.random() * mots.length)];
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .gros {
    font-size: 2em;
  }

  .success {
    color: green
  }

  .danger {
    color: red;
  }
</style>
