<template>
  <div class="container">
    <div v-if="recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.title }}</h1>
        <img :src="recipe.image" class="center" />
      </div>
      <div class="recipe-body">
        <div class="wrapper">
          <div class="wrapped">
            <div class="mb-3">
              <div><b>Ready in</b> {{ recipe.readyInMinutes }} minutes</div>
              <div><b>Likes:</b> {{ recipe.aggregateLikes }} likes</div>

              -----------------------

              <div v-if="recipe.vegan == 1" id="vegan" class="indication">
                <i class="fa fa-tree" aria-hidden="true"></i>
                <b>Vegan</b>
              </div>
              <div v-if="recipe.glutenFree == 1" id="gluten" class="indication">
                <i class="fa fa-pagelines" aria-hidden="true"></i>
                <b>Gluten Free</b>
              </div>

            </div>
            <!-- Ingredients:
            <ul>
              <li
                v-for="(r, index) in recipe.extendedIngredients"
                :key="index + '_' + r.id"
              >
                {{ r.original }}
              </li>
            </ul> -->
          </div>
          <div class="wrapped">
           <b> Instructions:</b>
            <ol>
              {{recipe.instructions}}
            </ol>
          </div>
        </div>
      </div>
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recipe: null,
      vegeterian: false,
      vegan: false,
      glutenFree: false
    };
  },
  async created() {
    try {
      // let response;
      // // response = this.$route.params.response;

      // try {
      //   response = await this.axios.get(
      //     "http://localhost:4000/users/displayMyRecipeInformation",       
      //     {
      //       params: { 
      //         recipe_id: this.$route.params.recipeId }
      //     }
      //   );

      //   // console.log("response.status", response.status);
      //   if (response.status !== 200) this.$router.replace("/NotFound");
      // } catch (error) {
      //   console.log("error.response.status", error.response.status);
      //   this.$router.replace("/NotFound");
      //   return;
      // }

      let {
        id,
        title,
        readyInMinutes,
        aggregateLikes,
        vegan,
        glutenFree,
        image,
        instructions,
        servings,
        extendedIngredients  
                
      } = this.$route.params.recipe;//todo: ?

      // let _instructions = analyzedInstructions
      //   .map((fstep) => {
      //     fstep.steps[0].step = fstep.name + fstep.steps[0].step;
      //     return fstep.steps;
      //   })
      //   .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        id,
        title,
        readyInMinutes,
        aggregateLikes,
        vegan,
        glutenFree,
        image,
        instructions,
        servings,
        extendedIngredients  
      };

      this.recipe = _recipe;
      this.checkIndications();
    } catch (error) {
      console.log(error);
    }
  },
  methods:{
    checkIndications() {
        if (this.recipe.vegetarian==1){
          this.vegeterian = true;
        }
        
        this.vegan = this.recipe.vegan;
        this.glutenFree = this.recipe.gluten_free;
      },
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
}
.wrapped {
  width: 50%;
}
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
/* .recipe-header{

} */
</style>
