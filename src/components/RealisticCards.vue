<template>
  <table class="organizecards">
    <tr>
      <td class>
        <!--BEGIN PIKACHU-->
        <div class="nameimageinfo lightning">
          <table class="nameheaders">
            <tr>
              <td class="basic" colspan="3">Basic Pokemon</td>
            </tr>
            <tr>
              <td class="nameofanimal">{{ props.pokemon.name }}</td>
              <td class="hp">60 HP</td>
              <td class="typesign">
                <img
                  src="https://heatherketten.files.wordpress.com/2018/03/nrg_electric.png"
                  width="30"
                  height="30"
                />
              </td>
            </tr>
          </table>
          <img
            class="headshot"
            :src="`${props.pokemon.sprites.other.home.front_default}`"
            alt="Pikachu"
          />
          <p class="description">Mouse Pokemon. Length 1'4", Weight 13 lbs.</p>
          <div class="infoonly">
            <table class="stats">
              <tr>
                <td class="energy">
                  <img
                    src="https://heatherketten.files.wordpress.com/2018/03/nrg_normal.png"
                    width="20"
                    height="20"
                  />
                </td>
                <td><span class="label">Growl</span> <span class="labeltext"> </span></td>
                <td class="damage">10</td>
              </tr>
            </table>
            <hr />
            <table class="stats">
              <tr>
                <td class="energy">
                  <img
                    src="https://heatherketten.files.wordpress.com/2018/03/nrg_electric.png"
                    width="25"
                    height="25"
                  /><img
                    src="https://heatherketten.files.wordpress.com/2018/03/nrg_electric.png"
                    width="25"
                    height="25"
                  />
                </td>
                <td>
                  <span class="label">Thundershock</span>
                  <span class="labeltext"
                    >Flip a coin. If tails, Pikachu does 10 damage to itself.</span
                  >
                </td>
                <td class="damage">30</td>
              </tr>
            </table>
            <hr />
            <table class="costs">
              <tr class="costheaders">
                <td>weakness</td>
                <td>resistance</td>
                <td>retreat cost</td>
              </tr>
              <tr class="costicons">
                <td>
                  <img
                    src="https://heatherketten.files.wordpress.com/2018/03/nrg_fire.png"
                    width="20"
                    height="20"
                  />
                </td>
                <td></td>
                <td>
                  <img
                    src="https://heatherketten.files.wordpress.com/2018/03/nrg_normal.png"
                    width="20"
                    height="20"
                  />
                </td>
              </tr>
            </table>
            <p class="italicize">
              When several of these Pokemon gather, their electricity could build and cause
              lightning storms.
            </p>
            <p class="bottomtext">
              <strong>Illus. Mitsuhiro Arita</strong> C 1995, 96, 98 Nintendo Creatures, GAMEFREAK C
              1999 Wizards. <strong>58/102 o</strong>
            </p>
          </div>
        </div>
        <!-- END PIKACHU -->
      </td>
    </tr>
  </table>
</template>

<script setup>
const props = defineProps({
  pokemon: {
    type: Object,
    required: true
  }
})
</script>

<style lang="scss" scoped>
p.italicize {
  font-style: italic;
  font-weight: bold;
  font-size: 11px;
  border: 3px solid gold;
  border-radius: 6px;
  margin: 0px;
  padding: 5px;
  text-align: center;
}

span.label {
  font-weight: bold;
  font-size: 16px;
}

ul {
  list-style-type: none;
  margin: 0px;
  padding: 0px;
}

div.nameimageinfo {
  width: 310px;
  height: 500px;
  padding: 10px;
  border: 10px solid gold;
  border-radius: 20px;
}

img.headshot {
  height: 150px;
  width: 300px;
  padding: 0px;
  margin: 0px;
  border: 5px yellow outset;
  box-shadow: 3px 3px 10px #000;
}

/* */
/* Just for fun - extra style things */

/* Background of entire page */
body {
  background-color: gray;
}

/* Background of water type cards */

div.water {
  background: linear-gradient(
    to bottom right,
    #d9e4ec,
    #adc1d1,
    #7d99af,
    #557792,
    #7d99af,
    #adc1d1
  );
}

/* Background of lightning type cards */

div.lightning {
  background: linear-gradient(
    to bottom right,
    #ffffa4,
    #fff870,
    #fff200,
    #fff870,
    #ffffa4,
    #fff870
  );
}

/* Background of fire type cards */

div.fire {
  background: linear-gradient(
    to bottom right,
    #ffbfba,
    #ff978f,
    #ff756b,
    #ff594c,
    #ff756b,
    #ff978f
  );
}

/* Background of grass type cards */

div.grass {
  background: linear-gradient(
    to bottom right,
    #aae5b7,
    #78cf8b,
    #4fb665,
    #319d49,
    #4fb665,
    #78cf8b
  );
}

/* Font styling */

div {
  font-family: sans-serif;
}

td.basic {
  font-weight: bold;
  font-size: 11px;
  margin: 0px;
  padding: 0px;
  width: 100%;
}

td.nameofanimal {
  font-weight: bold;
  font-size: 18px;
  margin: 0px;
  padding: 0px;
}

td.hp {
  color: crimson;
  font-size: 20px;
  text-align: right;
  font-weight: bold;
  width: 20%;
}

td.typesign {
  font-size: 20px;
  text-align: center;
  width: 5%;
}

p.description {
  padding: 2px 0px 0px 0px;
  margin: 0px 0px 5px 0px;
  background: linear-gradient(to right, goldenrod, yellow, goldenrod);
  font-size: 11px;
  font-family: sans-serif;
  font-style: italic;
  font-weight: bold;
  text-align: center;
}

span.labeltext {
  font-size: 11px;
}

td.energy {
  width: 18%;
  font-size: 20px;
  text-align: center;
}

td.damage {
  font-weight: bold;
  text-align: right;
}

table.costs {
  font-size: 11px;
  text-align: center;
  width: 100%;
}

tr.costheaders {
  font-weight: bold;
}

tr.costicons {
  font-size: 20px;
}

table.nameheaders {
  width: 100%;
}

table.stats {
  width: 100%;
  text-align: center;
}

p.bottomtext {
  font-size: 7px;
  text-align: center;
}
</style>
