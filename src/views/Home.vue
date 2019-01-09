<template>
  <div class="wrapper">
    <HeroImage v-if="step === 0"/>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput"/>
  </div>
</template>

<script>
import HeroImage from '@/components/HeroImage.vue';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
  components: {
    HeroImage,
    Claim,
    SearchInput,
  },
  data() {
    return {
      searchValue: '',
      results: [],
      loading: false,
      step: 0,
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    margin: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
  }
</style>
