<template>
  <base-card>
    <base-button @click="setSelectedTab('StoredResources')"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('AddResource')"
      >Add Resource</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },

  data() {
    return { selectedTab: 'StoredResources' };
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
  },
};
</script>
