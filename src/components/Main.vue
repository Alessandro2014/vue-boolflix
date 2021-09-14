<template>
  <div :id="id">
      <!-- STAMPA DINAMICA FILM/SERIE -->
    <h2 v-if="items.length > 0">{{ title }}</h2> 
    <!-- CICLO PER STAMPA ITEM -->
    <div v-for="(item, index) in items" :key="item.id + '-' + index">
        <SingleCard :item="item"/>
    </div>
  </div>
</template>

<script>
import SingleCard from '@/components/SingleCard.vue';
export default {
    name: "Main",
    props: ["id", "title", "items"],
    components: {
        SingleCard,
    },
    data() {
      return {
    };
  },
};
</script>

<style scoped lang="scss">
h2 {
    font-size: 38px;
    margin: 30px 10px;
    color: red;
    width: 100%;
    
}
</style>