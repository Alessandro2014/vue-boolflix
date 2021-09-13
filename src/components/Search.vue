<template>
  <div>

    <input type="text" :placeholder="placeholder"
        v-model.trim="inputValue" @keyup.enter="startSearch">
    <button type="submit" @click="startSearch">{{ buttonText || "Cerca" }}</button>
    <button @click="resetInput">{{ buttonReset || "Azzera" }}</button>
  </div>
</template>

<script>
export default {
name: "Search",
    data() {
        return {
        inputValue: "",
        };
    },
    props: ["placeholder", "buttonText", "buttonReset"],
    methods: {
        startSearch() {
            this.$emit("search", this.inputValue);
            this.resetInput();
        },

    resetInput() {
      this.inputValue = "";
    },
  },
};
</script>

<style scoped lang="scss">
// INPUT e BUTTON
input, button {
  padding: 5px 20px;
  margin: 0 10px;
}


</style>