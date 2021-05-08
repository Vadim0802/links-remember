<template>
  <base-card>
    <h2>Title</h2>
    <input required type="text" name="title" v-model="title" />
    <h2>Description</h2>
    <input required type="text" name="description" v-model="description" />
    <h2>Link</h2>
    <input required type="text" name="link" v-model="link" />
    <base-button @click="addRes">Add</base-button>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
      link: "",
    };
  },

  inject: ["addResource"],

  methods: {
    addRes() {
      const newRes = {
        id: new Date().toISOString(),
        title: this.title,
        description: this.description,
        link: this.link,
      };
      this.addResource(newRes);
    },
  },
};
</script>

<style scoped>
input {
  width: 100%;
}
</style>
