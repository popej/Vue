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
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Claim from "@/components/Claim";
import SearchInput from "@/components/SearchInput";
import HeroImage from "@/components/HeroImage";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput,
    HeroImage
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
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
  transition: opacity .5s ease;
}
.fade-enter,
.fade-leave {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top .5s ease;
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
</style>
