<template>
  <base-card>
    <div class="button-row">
      <base-button
        class="stored-resources-btn"
        :class="{ active: selectedTab === 'stored-resources' }"
        @click="setSelectedTab('stored-resources')"
        :mode="storedResButtonMode"
      >
        Stored Resources
      </base-button>

      <base-button
        @click="setSelectedTab('add-resource')"
        :mode="addResButtonMode"
      >
        Add Resource
      </base-button>
    </div>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
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
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'vue-3-official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js (Vue 3) documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>

<style>
.button-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

.button-row base-button:last-child {
  margin-left: auto;
}

.stored-resources-btn {
  font-weight: 600;
  color: black !important;
  font-family: inherit;
  font-size: 1rem;
}

.stored-resources-btn.active {
  color: white !important;
}
</style>
