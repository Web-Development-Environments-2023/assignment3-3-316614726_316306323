<template>
  <div class="container">
    <RecipePreviewList
      v-if="$root.store.username"
      title="Favorite Recipes"
      state="favorite"
      :class="{
        RandomRecipes: true,
        center: true,
      }"
    ></RecipePreviewList>
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";

export default {
  name: "favorite",
  components: { RecipePreviewList },
  data() {
    return {};
  },
  validations: {},
  methods: {},
};
</script>
<style lang="scss" scoped>
.container {
  max-width: 70%;
}
</style>
