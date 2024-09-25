<template>
  <base-card class="custom-centered-button">
    <base-button @click="setSelectedTab('stored-resource')"
                 :mode="storedResButtonMode">
      Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')"
                 :mode="addResButtonMode">
      Add Resource</base-button>
  </base-card>
  <!-- this is vue-container for rendering dynamic components (example: switching components): -->
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResource from '@/components/learning-resources/StoredResource.vue'
import AddResource from '@/components/learning-resources/AddResource.vue'

export default {
  components: { StoredResource, AddResource },
  data() {
    return {
      selectedTab: 'stored-resource',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official VueJS documentation.',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com'
        }
      ]
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource
    }
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resource' ? null : 'flat'
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat'
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url
      }
      this.storedResources.unshift(newResource) // push(), but on top
      this.selectedTab = 'stored-resource'
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId)
      this.storedResources.splice(resIndex, 1)
    }
  }
}
</script>

<style scoped>
.custom-centered-button {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
</style>