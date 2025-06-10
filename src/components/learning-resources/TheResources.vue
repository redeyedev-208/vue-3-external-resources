<template>
  <nav aria-label="Resource tabs navigation">
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
  </nav>

  <main aria-live="polite" aria-label="Selected resource content">
    <keep-alive>
      <component :is="selectedTab" />
    </keep-alive>
  </main>
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
    const saved = localStorage.getItem('resources');
    return {
      selectedTab: 'stored-resources',
      storedResources: saved
        ? JSON.parse(saved)
        : [
            {
              id: 'vue-3-official-guide',
              title: 'Official Guide',
              description: 'The official Vue.js (Vue 3) documentation',
              link: 'https://vuejs.org',
            },
            {
              id: '2025-06-10T04:12:34.548Z',
              title: 'Vue 3 CheatSheet For Developers',
              description: 'Put together by your friends at LearnVue',
              link: 'https://learnvue.co/LearnVue-Vue-3-Cheatsheet.pdf',
            },
            {
              id: '2025-06-10T04:14:40.236Z',
              title: 'Vue Cheat Sheet',
              description:
                'Vue Resources on Basic to Advanced workflows. Handling of Reactivity, Forms, Components, Composable, Routing and State Management with Pinia.',
              link: 'https://vue-cheatsheet.themeselection.com/vue/basic.html',
            },
            {
              id: '2025-06-10T04:15:44.281Z',
              title: 'Vue Cheat Sheet',
              description: 'Resources that are put together by DEV HINTS IO',
              link: 'https://devhints.io/vue',
            },
            {
              id: '2025-06-10T04:17:21.301Z',
              title: 'GitHub Vue Cheat Sheet',
              description: 'GitHub repository with lots of amazing information to reference when needed.',
              link: 'https://github.com/dekadentno/vue-cheat-sheet',
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
        title,
        description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.updateLocalStorage();
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const index = this.storedResources.findIndex(res => res.id === resId);
      if (index !== -1) {
        this.storedResources.splice(index, 1);
        this.updateLocalStorage();
      }
    },
    updateLocalStorage() {
      localStorage.setItem('resources', JSON.stringify(this.storedResources));
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
