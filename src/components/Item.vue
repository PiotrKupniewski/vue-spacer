<template>
  <div :style="style" class="item"></div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `background-image : url("${this.photo}")`;
    },
  },
};
</script>

<style lang="scss" scoped>
.item {
  min-width: 25vw;
  background-repeat: no-repeat;
  background-size: cover;
  width: auto;
  height: 250px;
  background-position: 50% 0;

  @media (min-wdith: 768) {
    width: 25vw;
  }
}
</style>
