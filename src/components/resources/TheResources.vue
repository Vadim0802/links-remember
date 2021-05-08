<template>
  <base-card>
    <base-button @click="changeCurrentTab('stored-resources')"
      >Stored Resources</base-button
    >
    <base-button @click="changeCurrentTab('add-resource')"
      >Add Resource</base-button
    >
  </base-card>
  <component :is="currentTabView"></component>
</template>

<script>
import { computed } from "vue";
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";

export default {
  components: {
    StoredResources,
    AddResource,
  },

  provide() {
    return {
      resources: computed(() => this.storedResources),
      deleteResource: this.deleteResource,
      addResource: this.addResource,
    };
  },

  data() {
    return {
      storedResources: [
        {
          id: "official-guide",
          title: "Official Guide",
          description: "The official Vue.js documentaiton",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn to Google",
          link: "https://google.com",
        },
      ],
      currentTabView: "stored-resources",
    };
  },

  methods: {
    changeCurrentTab(value) {
      this.currentTabView = value;
    },

    deleteResource(id) {
      this.storedResources = this.storedResources.filter(
        (item) => item.id !== id
      );
    },

    addResource(newResource) {
      this.storedResources.unshift(newResource);
      this.currentTabView = "stored-resources";
    },
  },
};
</script>
