<template>
  <div>
    <b-card
      v-if="image_load"
      :title="recipe.title"
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"
    >
      <router-link
        :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
        class="recipe-preview"
      >
        <b-card-img :src="recipe.image" />
      </router-link>
      <b-card-text>
        {{ recipe.readyInMinutes }} Minutes <br />
        {{ recipe.popularity }} Likes
        <div v-if="recipe.isVegan">Vegan 🌿</div>
        <div v-if="recipe.isVegetarian">Vegetarian 🥕</div>
        <div v-if="recipe.isGlutenFree">Gluten Free 🌾❌</div>
        <p v-if="recipe.isWatched">👁</p>
        <p v-if="recipe.isFavorite">❤️</p>
        <p v-else>
          <b-button
            v-if="!recipe.isFavorite && $root.store.username"
            variant="outline-danger"
            @click="addToFavorite"
            >Add to Favorites</b-button
          >
        </p>
      </b-card-text>

      <router-link
        :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
        class="recipe-preview"
      >
        <b-button variant="primary">Check this out!</b-button>
      </router-link>
    </b-card>
    <b-spinner v-else variant="primary"></b-spinner>
  </div>
</template>

<script>
export default {
  mounted() {
    // this.axios.get(this.recipe.image).then((i) => {
    //   this.image_load = true;
    // });
    this.image_load = true;
  },
  data() {
    return {
      image_load: false,
    };
  },
  props: {
    recipe: {
      type: Object,
      required: true,
    },
  },
  methods: {
    async addToFavorite() {
      try {
        let response;
        try {
          let response = await this.axios.post(
            this.$root.store.server_domain + `/users/favorites`,
            {
              recipeId: this.recipe.id,
            }
          );
          if (response.status !== 200) this.$router.replace("/NotFound");
        } catch (error) {
          console.log("error.response.status", error.response.status);
          this.$router.replace("/NotFound");
          return;
        }
        this.recipe.isFavorite = true;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
.recipe-preview {
  display: inline-block;
  width: 90%;
  height: 100%;
  position: relative;
  margin: 10px 10px;
}
.recipe-preview > .recipe-body {
  width: 100%;
  height: 200px;
  position: relative;
}

.recipe-preview .recipe-body .recipe-image {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  display: block;
  width: 98%;
  height: auto;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover;
}

.recipe-preview .recipe-footer {
  width: 100%;
  height: 50%;
  overflow: hidden;
}

.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}

.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
}

.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}
</style>
