<template>
  <Layout v-slot="{ searchText }">
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
          <v-tabs v-model="tab" grow>
            <v-tab>All Event</v-tab>
            <v-tab>Designning</v-tab>
            <v-tab>Developing</v-tab>
          </v-tabs>
        </v-col>
      </v-row>
    </v-container>

    <v-row class="justify-space-around">
      <v-card
        v-for="edge in getEvents(searchText)"
        :key="edge.node.id"
        class="mt-5"
        width="300"
      >
        <v-img
          class="white--text align-end"
          height="200px"
          :src="`http://localhost:1337${edge.node.thumbnail}`"
        />
        <v-card-title>{{ edge.node.title }}</v-card-title>

        <v-card-subtitle class="pb-0">{{
          formatDate(edge.node.date)
        }}</v-card-subtitle>

        <v-card-actions>
          <v-btn
            @click="$router.push(`/events/${edge.node.id}`)"
            color="orange"
            text
          >
            More Info
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
          thumbnail
          category
        }
      }
    }
  }
</page-query>

<script>
import moment from 'moment';

export default {
  metaInfo: {},
  data() {
    return {
      tab: 0,
      events: [],
    };
  },

  mounted() {
    this.events = this.$page.events.edges;
  },

  watch: {
    tab(val) {
      if (this.tab === 0) {
        this.showAllEvents();
      } else {
        this.showEventsByType(val);
      }
    },
  },

  methods: {
    showAllEvents() {
      this.events = this.$page.events.edges;
    },
    showEventsByType(val) {
      this.events = this.$page.events.edges.filter((edge) => {
        return edge.node.category === val;
      });
    },
    formatDate(date) {
      return moment(date).format('MMMM Do YYYY, h:mm a');
    },
    getEvents(searchText) {
      return this.events.filter((edge) => {
        return edge.node.title.toLowerCase().includes(searchText.toLowerCase());
      });
    },
  },
};
</script>

<style></style>
