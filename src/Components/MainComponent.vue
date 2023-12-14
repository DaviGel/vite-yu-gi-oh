<script>
import axios from 'axios';
import CardComponent from './CardComponent.vue';
import { store } from '../store';
import CardsFounded from './CardsFounded.vue';
import LoaderComponent from './LoaderComponent.vue';

export default {
  name: 'MainComponent',
  data() {
    return {
      store,
      archetypes: '',
      selectedArchetype: '',
    };
  },
  components: {
    CardComponent,
    CardsFounded,
    LoaderComponent,
  },
  mounted() {
    this.filteredCards();
    axios
      .get(`https://db.ygoprodeck.com/api/v7/archetypes.php`)
      .then((response) => {
        this.store.archs = response.data.map((obj) => obj.archetype_name);
      });
  },
  methods: {
    filteredCards() {
      if (this.selectedArchetype === '') {
        axios
          .get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
          .then((response) => {
            this.store.cards = response.data.data;
          });
      } else {
        axios
          .get(
            `https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=${this.selectedArchetype}&num=20&offset=0`
          )
          .then((response) => {
            this.store.cards = response.data.data;
          });
      }
      return this.store.cards;
    },
  },
};
</script>

<template>
  <main>
    <div class="container select">
      <div class="select-species">
        <label for="species"></label>
        <select name="specie" id="species" v-model="selectedArchetype">
          <option value="">Select Archetype</option>
          <option v-for="element in store.archs" :value="element">
            {{ element }}
          </option>
        </select>
      </div>
    </div>
    <div class="container">
      <div class="card">
        <CardsFounded :found="store.cards.length" class="founded" />
        <ul v-if="store.cards.length === 20">
          <li v-for="card in filteredCards()">
            <CardComponent
              :img="card.card_images[0].image_url"
              :name="card.name"
              :archetype="card.archetype"
            />
          </li>
        </ul>
        <div v-else>
          <div class="container">
            <LoaderComponent />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
@use '../assets/scss/partial/variables' as *;
main {
  .container {
    background-color: #fff;
    max-width: 1180px;
    margin: 0 auto;
    padding: 48px;
    &.select {
      background-color: $primary-color;
      padding: 25px 0 25px 12px;
      select {
        width: 160px;
        padding: 13px 0 13px 9px;
        border-radius: 7px;
        border: 1px solid #ced4da;
      }
    }
    .card {
      ul {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        gap: 25px;
        li {
          list-style: none;
          width: calc(100% / 5 - 25px);
          display: flex;
          flex-direction: column;
        }
      }
      .founded {
        background-color: #212529;
        color: #fff;
        padding: 20px 0 20px 19px;
        font-weight: bold;
      }
    }
  }
}
</style>
