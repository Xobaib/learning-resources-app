<template>
  <base-card>
    <base-button
      @click="setSelectedTab('StoredResources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('AddResource')" :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <KeepAlive>
    <component :is="selectedTab"></component>
  </KeepAlive>
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
    return {
      selectedTab: 'StoredResources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com',
        },
      ],
    };
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },

    addResource(title, description, url) {
      const newResource = {
        id: Math.floor(Math.random() * 10000),
        title: title.charAt(0).toUpperCase() + title.slice(1),
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'StoredResources';
    },
  },

  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'StoredResources' ? null : 'flat';
    },

    addResButtonMode() {
      return this.selectedTab === 'AddResource' ? null : 'flat';
    },
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
    };
  },
};
</script>
