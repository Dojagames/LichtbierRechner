<script>
const Lichtsekunde = 299_792_458;
export default {
    data() {
        return {
            bierlaenge: "",
            kippenlaenge: "",
            lichtbier: 1200*Lichtsekunde,
            nanolichtbier: 359.75,
            lichtkippe: 300*Lichtsekunde,
            nanolichtkippe: 89.94,
            meter: "",
            nLB: 0,
            nLK: 0,
        }
    },
    props: {
        
    },
    components: {
        
    },
    watch: {
        bierlaenge(){
           this.RenderAll();
        },

        kippenlaenge(){
          this.RenderAll();
        },

        meter(){
          this.RenderAll();
        }
    },
    mount: {
        
    },
    methods: {
      RenderAll(){
        const _bierSec = Math.floor(Math.abs(this.bierlaenge.replace(',', '.'))) * 60 + (Math.floor((Math.abs(this.bierlaenge.replace(',', '.')) * 60) % 60));
        this.lichtbier = (_bierSec * Lichtsekunde);
        this.nanolichtbier = (this.lichtbier * (10 ** (-9))).toFixed(2);

        const _kippenSec = Math.floor(Math.abs(this.kippenlaenge.replace(',', '.'))) * 60 + (Math.floor((Math.abs(this.kippenlaenge.replace(',', '.')) * 60) % 60));
        this.lichtkippe = (_kippenSec * Lichtsekunde);
        this.nanolichtkippe = (this.lichtkippe * (10 ** (-9))).toFixed(2);

        this.nLB = (this.meter / this.nanolichtbier).toFixed(3);
        this.nLK =(this.meter / this.nanolichtkippe).toFixed(3);
      }
    }
}
</script>

<template>
    <div id="wrapper">
      <div id="container">
        <h1>LichtBierRechner</h1>
        <div class="input"><input type="text" class="element" placeholder="Bierlaenge in Minuten" v-model="this.bierlaenge"></div>
        <div class="input"><input type="text" class="element" placeholder="Kippenlaenge in Minuten" v-model="this.kippenlaenge"></div>
        <div id="breaker"></div><div id="breaker"></div>
        <div id="Bier" class="output">
          <p>Bierlaenge: {{ this.bierlaenge }} Minuten</p>
          <p>Lichtbier: {{ this.lichtbier }} m</p>
          <p>NanoLichtbier Laenge: {{ this.nanolichtbier }} m</p>
        </div>
        <div id="Kippe" class="output">
          <p>Kippenlaenge: {{ this.kippenlaenge }} Minuten</p>
          <p>Lichtkippe: {{ this.lichtkippe }} m</p>
          <p>Nanolichtkippen Laenge: {{ this.nanolichtkippe }} m</p>
        </div>
        <div id="breaker"></div>
        <h2 style="text-align: center;">Meter zu Nanolichtbier</h2>
        <div class="input"><input type="text" class="element" placeholder="Meter" v-model="this.meter"></div>
        <div id="meter" class="output">
          <p>{{ this.nLB }} nanoLB</p>
          <p>{{ this.nLK }} nanoLK</p>
        </div>
      </div>
    </div>
</template>

<style>
    body{
      background-image: url("../src/assets/wp.png");
      color: white;
      margin: 0;
    }
    #wrapper{
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 20%;
      height: 80%;
    }

    #container{
      width: 100%;
      height: 100%;
      background-color: rgb(36 , 36, 36);
    }

    h1{
      padding-top: 5px;
      color: white;
      text-align: center;
    }

    .element{
      position: relative;
      left: 50%;
      transform: translateX(-50%);
      width: 80%;
      margin-bottom: 5px;
      color: white;
      width: 100%;
      text-align: center;
      border: none;
      outline: none;
      background-color: transparent;
    }
    
    .input{
      border: 1px solid white;
      border-radius: 12px;
      width: 60%;
      margin-left: 50%;
      transform: translateX(-50%);
      justify-self: center;
      margin-bottom: 10px;
      background-color: rgba(255, 255, 255, 0.1);
    }

    .output {
      text-align: center;
      margin-top: 20px;
      margin-bottom: 40px;
      border: 1px dashed white;
    }


    @media (orientation: portrait) {
      body{
        /* overflow: hidden; */
      }

      * {
        font-size: small;
      }
      #wrapper {
        width: 100%;
        height: 100%;
      }

      #container {
        background: none;
      }

      .output {
        width: fit-content;
        padding: 5px 15px;
        position: relative;
        left: 50%;
        transform: translateX(-50%);
      }

      h1 {
        padding-bottom: 45px;
      }

      #breaker {
        height: 27px;
      }
    }

</style>