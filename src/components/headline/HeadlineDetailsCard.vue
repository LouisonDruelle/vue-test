<template>
  <div>
    <v-card
        v-if="headline"
        class="mx-auto"
        max-width="800"
      >
        <v-img
          v-if="headline.urlToImage"
          height="300px"
          :src="headline.urlToImage"
        >
        </v-img>

        <v-img
          v-else
          height="300px"
          src="https://images.unsplash.com/photo-1506702315536-dd8b83e2dcf9?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80"
        >
        </v-img>

        <v-card-subtitle class="pb-0">
          {{ headline.publishedAt | date }}
        </v-card-subtitle>

        <v-card-title class="text--primary py-3">
          {{ headline.title }}
        </v-card-title>

        <v-card-text class="text--primary py-3">
          <div>{{ headline.content }}</div>
        </v-card-text>
        <v-card-text class="text--primary py-6" v-if="headline.author">
          Author: {{ headline.author }}
        </v-card-text>
      </v-card>
    <BackButton />
  </div>
</template>

<script>
import dayjs from 'dayjs';
import BackButton from '@/components/BackButton.vue';

export default {
  props: ['headline'],

  components: {
    BackButton,
  },

  mounted() {
    this.$store.dispatch('addHeadlineToHistory', {
      headline: this.headline,
    });
  },

  filters: {
    date(value) {
      if (!value) return null;
      return dayjs(value);
    },
  },
};
</script>
