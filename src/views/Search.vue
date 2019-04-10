<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="../assets/nasa.png" class="logo" v-if="step === 1">
    </transition>

    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Claim from "@/components/Claim";
import SearchInput from "@/components/SearchInput";
import HeroImage from "@/components/HeroImage";
import Item from "@/components/Item";
import Modal from "@/components/Modal";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

    handleInput: debounce(function() {
      console.log(this.searchValue);
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500)
  }
};
</script>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter,
.fade-leave {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top 0.5s ease;
}
.slide-enter,
.slide-leave {
  margin-top: -50px;
}

.logo {
  position: absolute;
  width: 15vw;
  top: 30px;
  left: 30px;

  @media (min-width: 768px) {
    width: 7vw;
  }
}

.wrapper {
  position: relative;
  display: flex;
  width: 100%;
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;

  &.flexStart {
    justify-content: flex-start;
  }
}

.results {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  margin-top: 50px;

  @media (min-width: 768px) {
    width: 90%;
    grid-template-columns: 1fr 1fr 1fr;
  }
}
</style>
