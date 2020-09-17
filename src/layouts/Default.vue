<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title>Eventer</v-toolbar-title>
      <v-col cols="12" sm="6" md="3">
        <v-text-field
          placeholder="Search"
          class="ml-8"
          outlined
          rounded
          dense
          hide-details
          style="max-width: 350px"
          prepend-inner-icon="mdi-magnify"
        />
      </v-col>
      <v-spacer></v-spacer>
      <v-btn>Create New Event</v-btn>
    </v-app-bar>
    <v-main>
      <slot />
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

<style></style>
