<template>
  <v-app>
    <!-- <header class="header">
      <strong>
        <g-link to="/">{{ $static.metadata.siteName }}</g-link>
      </strong>
      <nav class="nav">
        <g-link class="nav__link" to="/">Home</g-link>
        <g-link class="nav__link" to="/about/">About</g-link>
      </nav>
    </header> -->
    <!-- <p>{{ $static.metadata.siteDescription }}</p> -->
    <v-app-bar app>
      <v-toolbar-title><g-link to="/">Event-App</g-link></v-toolbar-title>

      <v-text-field
      v-model="searchText"
      @click:clear="searchText = ''"
        placeholder="Search event..."
        class="ml-8"
        style="max-width: 350px;"
        prepend-inner-icon="mdi-magnify"
        clearable
        outlined
        rounded
        dense
        hide-details
      />
      <v-spacer />
      <v-btn>Create Event</v-btn>
    </v-app-bar>
    <v-main>
          <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
      <slot :searchText="searchText"/>
        </v-col>
        </v-container>
    </v-main>
  </v-app>
</template>

<static-query>
query {
  metadata {
    siteName,
    siteDescription
  }
}
</static-query>

<script>
export default {
  data() {
    return {
      searchText: ''
    }
  }
}
</script>

<style scoped>
/* body {
  font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, sans-serif;
  margin: 0;
  padding: 0;
  line-height: 1.5;
}

.layout {
  max-width: 760px;
  margin: 0 auto;
  padding-left: 20px;
  padding-right: 20px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  height: 80px;
}

.nav__link {
  margin-left: 20px;
} */
.v-toolbar__title a {
  text-decoration: none;
  color: #000;
}
</style>
