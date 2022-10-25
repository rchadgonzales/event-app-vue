<template>
  <Layout v-slot="{ searchText }">
    <!-- Learn how to use images here: https://gridsome.org/docs/images -->
    <!-- <g-image alt="Example image" src="~/favicon.png" width="135" />

    <h1>Hello, world!</h1>

    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Pariatur excepturi labore tempore expedita, et iste tenetur suscipit explicabo! Dolores, aperiam non officia eos quod asperiores
    </p>

    <p class="home-links">
      <a href="https://gridsome.org/docs/" target="_blank" rel="noopener">Gridsome Docs</a>
      <a href="https://github.com/gridsome/gridsome" target="_blank" rel="noopener">GitHub</a>
    </p> -->
    <!-- <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3"> -->
    <v-tabs v-model="tab" grow>
      <v-tab>All Events</v-tab>
      <v-tab>Music Events</v-tab>
      <v-tab>Coding Events</v-tab>
    </v-tabs>
    <v-row class="justify-space-around">
      <v-card
        v-for="edge in getEvents(searchText)"
        :key="edge.node.id"
        width="300"
        class="mt-5"
      >
        <v-img
          class="white--text align-end"
          height="200px"
          :src="`http://localhost:1337${edge.node.thumbnail}`"
        />
        <v-card-title>{{ edge.node.title }}</v-card-title>

        <v-card-subtitle class="pb-0">
          {{ formatDate(edge.node.date) }}
        </v-card-subtitle>

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
    <!-- </v-col>
      </v-row>
    </v-container> -->
  </Layout>
</template>

<page-query>
query {
  events: allEvent {
    edges {
      node {
        id
        title
        description
        price
        duration
        date
        thumbnail
        image
        category
      }
    }
  }
}
</page-query>

<script>
import moment from "moment";

export default {
  metaInfo: {
    title: "Hello, world!",
  },
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
      // console.log("showEvents");
      this.events = this.$page.events.edges;
    },
    showEventsByType(val) {
      // console.log("showEventsType");
      this.events = this.$page.events.edges.filter((edge) => {
        return edge.node.category === val;
      });
    },
    formatDate(date) {
      return moment(date).format("MMMM Do YYYY, h:mm a");
    },
    getEvents(searchText) {
      return this.events.filter((edge) => {
        return edge.node.title.toLowerCase().includes(searchText.toLowerCase());
      });
    },
  },
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
