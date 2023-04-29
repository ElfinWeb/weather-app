<template>
  <section class="input-part">
    <p class="info-txt"></p>
    <div class="content">
      <input
        type="text"
        spellcheck="false"
        placeholder="Enter city name"
        required
        v-model.trim="inputData"
      />
      <div class="separator"></div>
      <button @click="submitData">Submit</button>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      inputData: "",
    };
  },
  methods: {
    submitData() {
      if (this.inputData) {
        this.$emit("submit-data", this.inputData);
      }
    },
  },
};
</script>
