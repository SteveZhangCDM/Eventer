<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
          <v-tabs v-model="tab" grow>
            <v-tab>Item One</v-tab>
            <v-tab>Item Two</v-tab>
            <v-tab>Item Three</v-tab>
          </v-tabs>
        </v-col>
      </v-row>
    </v-container>

    <v-row class="justify-space-around">
      <v-card
        v-for="edge in $page.events.edges"
        :key="edge.node.id"
        class="mt-5"
        width="400"
      >
        <v-img
          class="white--text align-end"
          height="200px"
          src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
        >
          <v-card-title>{{ edge.node.title }}</v-card-title>
        </v-img>

        <v-card-subtitle class="pb-0">{{ edge.node.date }}</v-card-subtitle>

        <v-card-actions>
          <v-btn color="orange" text>
            More Info
          </v-btn>

          <v-btn color="orange" text>
            Explore
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-row>
  </Layout>
</template>

<page-query>
  query {
    events: allEvent{
      edges{
        node{
          id
          title
          description
          price
          date
          duration
        }
      }
    }
  }
</page-query>

<script>
export default {
  metaInfo: {},
  data() {
    return {
      tab: 0,
    };
  },
  watch: {
    tab(val) {
      if (this.tab === 0) {
        this.showAllEvents();
      } else {
        this.showEventsByType();
      }
    },
  },
  methods: {
    showAllEvents() {
      console.log('all');
    },
    showEventsByType() {
      console.log('type');
    },
  },
};
</script>

<style></style>
