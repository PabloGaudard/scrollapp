<template>
  <div id="navigation">
    <div v-for="i in length" :key="i" :class="{ active: index == i }"></div>
  </div>
</template>

<script>
export default {
  props: ["length", "index"],
};
</script>

<style lang="scss">
#navigation {
  position: fixed;
  right: 15px;
  top: 50%;
  display: flex;
  flex-flow: column;
  align-items: flex-end;

  div {
    height: 5px;
    width: 25px;
    background-color: rgba(255, 255, 255, 0.527);
    margin-bottom: 10px;

    transition: all 0.5s;

    &.active {
      background-color: #fff;
      width: 40px;
    }
  }
}
</style>