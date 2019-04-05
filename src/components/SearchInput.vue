
<template>
  <input id="search" name="search" :value="value" :class="{ dark }" @input="handleChange" autocomplete="off"/>
</template>

<script>
export default {
  name: "SearchInput",
  props: {
    value: {
      type: String,
      required: true
    },
    dark: {
        type: Boolean,
        default: false
    }
  },
  methods: {
      handleChange(e) {
          this.$emit('input', e.target.value);
      }
  },
};
</script>
<style lang="scss" scoped>
input {
  width: 300px;
  display: flex;
  flex-direction: column;
  margin-top: 5vh;

  color: #fff;
  height: 30px;
  text-align: center;
  font-size: 18px;
  font-weight: 200;
  border: 0;
  border-bottom: 1px solid #fff;
  background: none;
  transition: box-shadow 0.3s ease-out;

  &:focus {
    outline: none;
    box-shadow: 0 10px 10px -8px rgba(255, 255, 255, 0.5);
  }
}

.dark {
    color: #1e3d4a;
    border-bottom-color: #1e3d4a;

    &:focus {
        box-shadow: 0 10px 20px -8px rgba(255, 255, 255, .5)
    }
}
</style>
