<template>
  <div :id="id">
      <h2>{{title}}</h2>
    <ul v-for="(item, index) in items" :key="item.id + '-' + index">
          <SingleCard :item="item"/>
    </ul>
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
  methods: {}

  
};
</script>

<style scoped lang="scss">

h2 {
    text-align: center;
    font-size: 28px;
    margin-top: 30px;
}
.cover:hover {
  display: none;
  background-color: chartreuse;
}
</style>