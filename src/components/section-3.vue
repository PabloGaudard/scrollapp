<template>
  <section>
    <template v-for="i in texts.length">
      <p v-bind:key="i" v-bind:class="{ show: index == i }">
        {{ texts[i - 1] }}
      </p>
    </template>
  </section>
</template>

<script>
export default {
  data() {
    return {
      index: 1,
      texts: [
        `3. Rising seas are threatening the Marshall Islands, 
        a low-lying islandnation in the middle of the Pacific Ocean.`,
        `4. Vestibulum consectetur consequat eros, id dignissim massa pretium at.
        Aenean commodo neque sed molestie mattis.`,
      ],
    };
  },
};
</script>