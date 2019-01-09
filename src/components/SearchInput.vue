<template>
  <input
    class="search"
    name="search"
    :value="value"
    :class="{ dark }"
    @input="handleChange"
  />
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
  .search {
    height: 30px;
    border: 0;
    border-bottom: 1px solid #fff;
    background: none;
    transition: box-shadow .5s;
    color: #fff;
    text-align: center;
    font-size: 18px;
    font-weight: 400;
    padding-bottom: 5px;
    width: 220px;
    margin-top: 50px;

    @media (min-width: 768px) {
      width: 300px;
    }

    @media (min-width: 1024px) {
      font-size: 24px;
      width: 400px;
    }

    &:focus {
      outline: none;
      box-shadow: 0 14px 20px -10px rgba(255,255,255,.6);
    }

    &.dark {
      color: #111;
      border-bottom-color: #111;

      &:focus {
        box-shadow: 0 14px 20px -10px rgba(#111,.3);
      }
    }
  }
</style>
