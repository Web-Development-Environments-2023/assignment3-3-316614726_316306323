<template>
  <div id="main-container">
    <!-- <h1 id="main-title" class="title">Welcome To The Main Page!</h1> -->
    <div class="row vertical-align" style="flex-wrap:nowrap;">
      <div class="col-xs-6 col-md-6">
        <RecipePreviewList
          title="Explore This Recipes"
          class="RandomRecipes center"
          state="random"
        />
        <!-- <router-link v-if="!$root.store.username" to="/login" tag="button"
      >You need to Login first!</router-link
    > -->
      </div>
      <div class="col-xs-6 col-md-6">
        <Login v-if="!$root.store.username" />

        <!-- {{ !$root.store.username }} -->
        <RecipePreviewList
          v-else
          title="Last Watched Recipes"
          state="lastWatched"
          :class="{
            RandomRecipes: true,
            center: true,
          }"
        ></RecipePreviewList>
      </div>
      <!-- <div
      style="position: absolute;top: 70%;left: 50%;transform: translate(-50%, -50%);"
    >
      Centeredasdasdad
    </div>-->
    </div>
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import Login from "../components/Login";

export default {
  components: {
    RecipePreviewList,
    Login,
  },
};
</script>

<style lang="scss" scoped>
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}

#main-container {
  background-image: url("../assets/main-background.jpg");
  background-size: cover;
}

* {
  text-align: center;
}
h1 {
  font-size: 100px;
}
.vertical-align {
  display: flex;
  justify-content: center;
  flex-direction: row;
}

.vertical-align > div:last-child {
  margin-top: 17px;
}
</style>
