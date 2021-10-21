<template>
  <div>
    <template v-for="i in sections.length">
      <component
        :is="sections[i - 1]"
        :key="i"
        :ref="i"
        :class="{ show: index == i }"
      />
    </template>
    <Navigation :length="sections.length" :index="index"></Navigation>
  </div>
</template>

<script>
export default {
  components:{Navigation:()=> import('../components/Navigation.vue')},
  data() {
    return {
      index: 1,
      sections: [
        () => import(`../components/section-1.vue`),
        () => import(`../components/section-2.vue`),
        () => import(`../components/section-3.vue`),
      ],
    };
  },
  mounted() {
    window.addEventListener("keydown", this.handleNavigation);
  },
  destroyed() {
    window.removeEventListener("keydown", this.handleNavigation);
  },
  methods: {
    handleNavigation(event) {
      var section = this.$refs[this.index][0];
      if (event.keyCode == 40) {
        if (section.index < (section.texts || {}).length) section.index++;
        else if (this.index < this.sections.length) this.index++;
      } else if (event.keyCode == 38) {
        if (section.index > 1) section.index--;
        else if (this.index > 1) this.index--;
      }
    },
  },
};
</script>

<style lang="scss">
section {
  width: 100%;
  height: 100%;
  position: absolute;
  transition: opacity 1.5s;
  opacity: 0;
  padding: 50px;

  &:nth-of-type(1) {
    background-color: dodgerblue;
  }
  &:nth-of-type(2) {
    background-color: green;
  }
  &:nth-of-type(3) {
    background-color: orange;
  }
  &.show {
    opacity: 1;
  }

  p {
    background-image: url("../assets/texture.png");
    padding: 20px;
    text-shadow: 0px 0px 0.4em rgb(0 0 0 / 60%);
    font-weight: 800;
    font-size: 1.2rem;
    line-height: 1.8rem;
    position: absolute;
    max-width: 80%;

    transition: all 1.5s;
    transform: translateY(40px);
    opacity: 0;

    &.show {
      opacity: 1;
      transform: translateY(0);
    }
  }
}
</style>