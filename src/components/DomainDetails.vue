<template>
  <div style="margin-top: 7px">
    <v-card
      color="teal-darken-4"
      class="mx-auto"
      max-width="544"
      variant="elevated"
      image="https://picsum.photos/1920/1080?random"
    >
      <v-card-title class="text-h5"> Information </v-card-title>
      <v-card-subtitle>
        Showing domain and we pages of selected univeristy
      </v-card-subtitle>
      <v-card-item>
        <div>
          <div class="text-h6 mb-1 d-flex py-3 justify-space-between">
            Domains
          </div>
          <v-list density="compact">
            <v-list-item
              v-for="(item, i) in domains"
              :key="i"
              :value="item"
              color="primary"
            >
              <v-list-item-title v-text="item"></v-list-item-title>
            </v-list-item>
          </v-list>
          <v-divider></v-divider>
          <div class="text-h6 mb-1 d-flex py-3 justify-space-between">
            Web Pages
          </div>
          <v-list density="compact">
            <v-list-item
              v-for="(item, i) in webpages"
              :key="i"
              :value="item"
              color="primary"
            >
              <v-list-item-title v-text="item"></v-list-item-title>
            </v-list-item>
          </v-list>
        </div>
      </v-card-item>
    </v-card>
  </div>
</template>
<script>
export default {
  name: "DomainDetails",
  props: {
    domains: {
      type: Array,
      required: true,
    },
    webpages: {
      type: Array,
      required: true,
    },
  },
};
</script>
