<template>
  <input
    id="search"
    name="search"
    :class="{ dark }"
    :value="value"
    @input="handleInputChange"
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
    handleInputChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
input {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  width: 400px;
  text-align: center;
  background: none;
  height: 100px;
  border: 0;
  border-bottom: 1px solid #fff;
  color: #fff;
  font-size: 50px;
  transition: box-shadow 0.5s ease-out;
}

input:focus {
  outline: none;
  box-shadow: 0px 10px 30px -15px rgba(255, 255, 255, 0.3);
}

.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;
}

.dark:focus {
  outline: none;
  box-shadow: 0px 10px 30px -15px rgba(#1e3d4a, 0.3);
}
</style>
