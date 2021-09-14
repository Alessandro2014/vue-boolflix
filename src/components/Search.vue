<template>
  <div>
    <!-- CAMPO DI SCRITTURA -->
    <input type="text" :placeholder="placeholder"
        v-model.trim="inputValue" @keyup.enter="startSearch">
        <!-- BOTTONE CERCA -->
    <button type="submit" @click="startSearch">{{ buttonText || "Cerca" }}</button>
    <!-- BOTTONE DI AZZERAMENTO INPUT -->
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
          // TRASFERIMENTO SCELTA UTENTE AL PADRE
            this.$emit("search", this.inputValue);
            this.resetInput();
        },
    // METODO PER PULIZIA CAMPO INPUT
    resetInput() {
      this.inputValue = "";
    },
  },
};
</script>

<style scoped lang="scss">
// INPUT e BUTTON
input {
  padding: 5px 20px;
    margin: 5px;
}

button {
  padding: 5px 10px;
  margin: 5px;
}


</style>