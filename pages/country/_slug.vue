<template>
  <div>
    <v-row id="controls">
      <v-col
        v-for="buttonLabel in ['confirmed', 'deaths']"
        :key="buttonLabel"
      >
        <v-btn
          block
          style="margin-top: 0; padding-top: 0"
          @click="dataLabel = buttonLabel"
        >
          {{ buttonLabel }}
        </v-btn>
      </v-col>
    </v-row>
    <chart
      :data="$store.getters[dataLabel]"
      :labels="$store.getters.labels"
      :data-label="dataLabel"
    />
  </div>
</template>

<script>
import Chart from '~/components/Chart.vue';

export default {
  components: { Chart },
  data() {
    return {
      dataLabel: 'confirmed',
    };
  },
  created() {
    this.$store.dispatch('getCountry', this.$route.params.slug);
  },
};
</script>

<style></style>
