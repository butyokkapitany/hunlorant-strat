<template>
  <div class="container">
    <div class="focim">
      <h1>
        Üdvözöllek a magyar Valorant Strat Roulette oldalon!
      </h1>
    </div>
    <div class="leiras">
      <h2>
        Szükségetek lenne egy kis funolásra? Megvan a teljes csapat, de már
        unjátok a játékmódokat? Ez az oldal azért jött létre, hogy egy kis
        szórakozást vigyen a hétköznapok unalmába.
      </h2>
      <h3>
        Az oldalt mindenki csak saját felelősségre használja!
        Csak unrated meccseken használjátok, sose rankedezzetek ezekkel a szabályokkal.
        Ajánlott, ha 5-en vagytok, illetve Voice Chatet is használtok.
      </h3>
    </div>
    <div>
      <p>
        Készítette: <a href="https://twitch.tv/butyokkapitany"
        class="link" target="_blank">@butyokkapitany</a>
      </p>
      <p>
        Ha van további ötleted, írj
        <a href="mailto:butyokbot@gmail.com" class="link">
          e-mailt
        </a>
        , vagy nyiss egy Pull Requestet Githubon
      </p>
    </div>
      <div class="side-picker">
      <label for="attack" class="attack" :class="{'a-selected': picked==='attack'}">Attack
        <input type="radio" name="attack" id="attack" value="attack" v-model="picked"
        @change="newRule()" />
      </label>
      <label for="defense" class="defense" :class="{'d-selected': picked==='defense'}">Defense
        <input type="radio" name="defense" id="defense" value="defense" v-model="picked"
        @change="newRule()" />
      </label>
      </div>
    <button @click.prevent="newRule()" class="newRuleBtn" v-if="selectedRule">Strat</button>
        <transition-group name="list">
    <div v-if="selectedRule" class="rule" :key="selectedRule.name">
      <h3 class="rule-name">
        {{ selectedRule.name }}
      </h3>
      <p class="rule-text">
        {{ selectedRule.description }}
      </p>
      <p v-if="selectedRule.altText">
        {{ selectedRule.altText }}
      </p>
    </div>
    </transition-group>
  </div>
</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue';

const picked = ref();

type Rule = {
  name: string,
  description: string,
  altText?: string,
}
const ARules: Rule[] = [
  {
    name: 'Odin Mester',
    description: 'Mindenki Odin-t vásárolhat csak',
  },
  {
    name: 'Precise Gunplay BTW',
    description: 'Csak futás közben lőhettek',
  },
  {
    name: 'Pókembej, pókembej...',
    description: 'Csak a falhoz érve mozoghattok',
    altText: 'Az ajtókat átugorhatjátok',
  },
  {
    name: 'Multimilliomos',
    description: 'A legtöbb pénzzel rendelkező játékos vesz mindenki másnak fegyvert',
  },
  {
    name: 'Bunnyhop Mester',
    description: 'Mindenkinek ugrálva kell bemennie a bombalerakóhoz',
  },
  {
    name: 'FantUwUsztikus!',
    description: 'Mindenkinek UwU-t kell mondania a mondatai végén',
  },
  {
    name: 'Motivált Játékos',
    description: 'Csak a Bottom Frag léphet be először a bombalerakóhoz',
  },
  {
    name: 'Deadweight',
    description: 'A Top Frag nem vehet semmit',
  },
  {
    name: 'Morálnövelés',
    description: 'Ha valaki kill-t szerez a csapatban, mindenki másnak meg kell őt dícsérnie',
    altText: 'De nagyon kínosan...',
  },
  {
    name: 'Tisztára Mint A Profik',
    description: 'Csak "A" és "D" billentyűkkel mozoghattok',
  },
  {
    name: 'Mindent Vagy Semmit',
    description: 'Ha csak 1 játékos él az ellenségnél, mindenkinek őt kell vadásznia',
    altText: 'Nem rakhatjátok le a bombát, ha még nem került le',
  },
  {
    name: 'Majdnem Hasbeszélő',
    description: 'Mindenkinek utánoznia kell a fegyverének a hangját lövés közben',
  },
  {
    name: 'Stinger Rush',
    description: 'Csak Stinger-t vehettek',
  },
  {
    name: 'Anime CS:GO',
    description: 'Nem használhattok képességet',
  },
  {
    name: 'Majdnem Call Of Duty',
    description: 'Csak ADS-t használva lőhettek',
    altText: 'ADS: Aim Down Sights - jobb klikk',
  },
  {
    name: 'Fő A Változatosság',
    description: 'Mindenkinek fegyvert kell cserélnie egymással',
  },
  {
    name: 'Zsákbamacska',
    description: 'Mindnekinek le kell dobnia egy helyre a fegyverét, majd egyszerre át kell rajta sétálnotok',
  },
  {
    name: 'Rosszindulatú Játékos',
    description: 'Minden megölt ellenséget le kell spray-elnetek',
  },
  {
    name: 'Rezsicsökkentés',
    description: 'Ebben a körben nem vehettek semmit',
  },
  {
    name: 'You Only YOLO Once',
    description: 'Maximum egér érzékenység',
  },
  {
    name: 'Blaha Szimulátor',
    description: 'Az utolsó ellenséget késsel kell megölnötök',
  },
  {
    name: 'Honfoglalás',
    description: 'Csak az ellenfél spawn helyének érintése után rakhatjátok le a bombát',
  },
];
const DRules: Rule[] = [
  {
    name: 'Teamwork OP',
    description: 'Mindenki csak 1 siteon lehet',
  },
  {
    name: 'A Mesterlövész',
    description: 'Mindenkinél csak sniper lehet',
    altText: 'Marshal & Operator',
  },
  {
    name: 'Extraprofit',
    description: 'Mindenkinek másik fegyvert kell vennie',
  },
  {
    name: 'Fake News',
    description: 'Ha megláttok egy ellenfelet, csak olyan helyet mondhattok, ahol nincsenek',
  },
  {
    name: '47-es Ügynök',
    description: 'Csak hangtompítós fegyvereket használhattok és csak sétálva közlekedhettek',
  },
  {
    name: 'Hasta La Vista, Baby',
    description: 'Mindenkinél csak shotgun lehet',
    altText: 'Bucky, Judge, Shorty',
  },
  {
    name: 'Iz Der Eni Kvescsön?',
    description: 'Csak angolul kommunikálhattok ebben a körben',
  },
  {
    name: 'Tik-tak',
    description: 'Csak a bomba lerakása után mehettek el a spawn területéről',
  },
  {
    name: 'X-Men',
    description: 'Csak képességgel ölhetsz meg ellenfelet',
    altText: 'Ha nincs sebző képessége valakinek, akkor pisztollyal',
  },
  {
    name: 'First Blood',
    description: 'Aki először öl meg egy ellenfelet, el kell dobnia a fegyverét és mindenki más csak azzal a fegyverrel ölhet',
  },
  {
    name: 'Soros-terv',
    description: 'Jelöljetek ki valakit vezérnek. Csak akkor kezdhettek lőni, ha ő engedélyt adott rá',
  },
  {
    name: 'A Bárányok Hallgatnak',
    description: 'A csapatból mindenkinek 0-ra kell állítani a játék hangerejét',
  },
  {
    name: 'A Számok Bűvöletében',
    description: 'Mindenki csak annyi golyót lőhet újratöltés nélkül, ahány ölése van',
  },
  {
    name: 'Valódi Stereo',
    description: 'Mindenki fordítsa meg a headsetjét',
  },
  {
    name: 'A Valorant-tenger Kalózai',
    description: 'Mindenki csukja le az egyik szemét',
    altText: 'Aki szemüveges, az vegye le a szemüvegét',
  },
];

const selectedRule: Ref<Rule | undefined> = ref();

function getRandomInt(max: number): number {
  return Math.floor(Math.random() * max);
}

function newRule(): void {
  selectedRule.value = picked.value === 'attack' ? ARules[getRandomInt(ARules.length)] : DRules[getRandomInt(DRules.length)];
}
</script>

<style scoped>
.container {
  margin: 20px;
}

.focim {
  text-align: center;
}

.side-picker {
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  font-family: Valorant;
  font-size: 4rem;
}

.attack {
  border-radius: 20px;
  text-align: center;
  padding: 1rem;
  margin-bottom: 2rem;
  background-color: var(--accent3);
}

.defense {
  border-radius: 20px;
  text-align: center;
  padding: 1rem;
  margin-bottom: 2rem;
  background-color: var(--accent4);
}

.rule {
  word-wrap: break-word;
  position: absolute;
  margin: 20px;
  padding: 0;
  left: 0;
  right: 0;
  text-align: center;
}

.rule-name {
  color: var(--accent2);
  font-size: 4rem;
  margin-bottom: -50px;
}

.rule-text {
  font-size: 3rem;
  margin-bottom: -10px;
}
.side-picker input {
  display: none;
}
.side-picker label {
  cursor: pointer;
}
.a-selected {
  box-shadow: 0px 0px 30px var(--accent3);
}
.d-selected {
  box-shadow: 0px 0px 30px hsl(216, 31%, 50%);
}
.newRuleBtn {
  position: relative;
  margin: auto;
  padding: 5px;
  border: 0;
  display: flex;
  background-color: var(--accent2);
  font-family: Valorant;
  color: var(--text);
  font-size: 4rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 300ms ease;
}
.newRuleBtn:hover {
  transform: scale(1.1);
  box-shadow: 0px 0px 15px var(--accent3);
}
.list-enter-active,
.list-leave-active {
  transition: all 300ms ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
}
.link {
  font-weight: bold;
  color: var(--accent3);
}
.leiras {
  text-align: center;
}
</style>
