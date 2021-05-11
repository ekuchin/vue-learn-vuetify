<template>
  <div class="about">
    <h1>This is an about page</h1>

    <v-card class="ma-5 pa-5">
      <v-card-title>Имя кота</v-card-title>
      <v-card-text>{{ catname }}</v-card-text>
      <v-card-actions>
        <v-btn>Погладить</v-btn>
      </v-card-actions>
    </v-card>

    <v-card class="ma-5 pa-5">
      <v-text-field label="Имя кота" type="text" v-model="catname" />
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => {
    return { catname: "Мурзик" };
  },
};
</script>
