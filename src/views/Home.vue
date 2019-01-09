<template>
  <div :class="[{ 'flex-start': step === 1 }, 'wrapper']">
    <transition name="slide">
      <p class="logo" v-if="step === 1">spacer journey</p>
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step ===1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
    </div>
    <div class="loader" v-if="step === 1 && loading">
      <div class="lds-ellipsis"><div></div><div></div><div></div><div></div></div>
    </div>
    <DetailsModal v-if="modalOpened" :item="modalData" @closeModal="modalOpened = false"/>
  </div>
</template>

<script>
import HeroImage from '@/components/HeroImage.vue';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import Item from '@/components/Item.vue';
import DetailsModal from '@/components/DetailsModal.vue';
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
  components: {
    HeroImage,
    Claim,
    SearchInput,
    Item,
    DetailsModal,
  },
  data() {
    return {
      searchValue: '',
      results: [],
      loading: false,
      step: 0,
      modalOpened: false,
      modalData: null,
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpened = true;
      this.modalData = item;
    },
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .75s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .75s ease;
  }

  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

  .wrapper {
    position: relative;
    margin: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;

    &.flex-start {
      justify-content: flex-start;
    }

    .logo {
      position: absolute;
      top: 20px;
      font-size: 32px;
      font-weight: 700;
      text-transform: uppercase;
    }

    .results {
      width: 100%;
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 20px;
      margin-top: 40px;

      @media (min-width: 360px) {
        grid-template-columns: 1fr 1fr;
      }

      @media (min-width: 768px) {
        grid-template-columns: 1fr 1fr 1fr;
      }
    }
  }

  .loader {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    .lds-ellipsis {
      display: inline-block;
      position: relative;
      width: 64px;
      height: 64px;
    }
    .lds-ellipsis div {
      position: absolute;
      top: 27px;
      width: 11px;
      height: 11px;
      border-radius: 50%;
      background: #111;
      animation-timing-function: cubic-bezier(0, 1, 1, 0);
    }
    .lds-ellipsis div:nth-child(1) {
      left: 6px;
      animation: lds-ellipsis1 0.6s infinite;
    }
    .lds-ellipsis div:nth-child(2) {
      left: 6px;
      animation: lds-ellipsis2 0.6s infinite;
    }
    .lds-ellipsis div:nth-child(3) {
      left: 26px;
      animation: lds-ellipsis2 0.6s infinite;
    }
    .lds-ellipsis div:nth-child(4) {
      left: 45px;
      animation: lds-ellipsis3 0.6s infinite;
    }
  }

  @keyframes lds-ellipsis1 {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
  @keyframes lds-ellipsis3 {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
  }
  @keyframes lds-ellipsis2 {
    0% {
      transform: translate(0, 0);
    }
    100% {
      transform: translate(19px, 0);
    }
  }
</style>
