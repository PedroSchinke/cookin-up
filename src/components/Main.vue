<script lang="ts">
import SelectIngredients from './SelectIngredients.vue';
import Tag from './Tag.vue';

export default {
  data() {
    return {
      ingredients: [] as string[]
    }
  },
  components: { SelectIngredients, Tag },
  methods: {
    addIngredient(ingredient: string) {
      this.ingredients.push(ingredient)
    },

    removeIngredient(ingredientToRemove: string) {
      const ingredientsWithoutRemovedOne = this.ingredients.filter(ingredient => ingredient !== ingredientToRemove)
      this.ingredients = ingredientsWithoutRemovedOne
    }
  }
}
</script>

<template>
  <main class="main">
    <section>
    <span class="subtitle-lg your-list-text">
      Sua lista:
    </span>

    <ul v-if="ingredients.length" class="your-list-ingredients">
      <li v-for="ingredient in ingredients" :key="ingredient">
        <Tag :text="ingredient" active/>
      </li> 
    </ul>

    <p v-else class="paragraph empty-list">
      <img src="../assets/images/icons/empty-list.svg" alt="">
      Your list is empty, select ingredients to begin.
    </p>
    </section>

    <SelectIngredients @add-ingredient="addIngredient($event)" @remove-ingredient="removeIngredient($event)"/>
  </main>
</template>

<style scoped>
  .main {
    padding: 6.5rem 7.5rem;
    border-radius: 3.75rem 3.75rem 0rem 0rem;
    background: var(--creme, #FFFAF3);
    color: var(--cinza, #444);

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5rem;
  }

  .your-list-text {
    color: var(--coral, #F0633C);
    display: block;
    text-align: center;
    margin-bottom: 1.5rem;
  }

  .your-list-ingredients {
    display: flex;
    justify-content: center;
    gap: 1rem 1.5rem;
    flex-wrap: wrap;
  }

  .empty-list {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 0.25rem;

    color: var(--coral, #F0633C);
    text-align: center;
  }

  @media only screen and (max-width: 1300px) {
    .main {
      padding: 5rem 3.75rem;
      gap: 3.5rem;
    }
  }

  @media only screen and (max-width: 767px) {
    .main {
      padding: 4rem 1.5rem;
      gap: 4rem;
    }
  }
</style>