<template>
  <ul>
    <learning-resource v-for="res in resources"
                       :key="res"
                       :id="res.id"
                       :title="res.title"
                       :description="res.description"
                       :link="res.link">{{ res.id }}
    </learning-resource>
  </ul>
</template>

<script>
import LearningResource from '@/components/learning-resources/LearningResource.vue';

export default {
  inject: ['resources'],
  components: {
    LearningResource,
  },
  data() {
    return {

    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>