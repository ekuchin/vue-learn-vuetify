<template>
  <div class="about">
    <h1>This is an about page</h1>

    <v-card class="ma-5 pa-5">
      <v-card-title>Имя кота</v-card-title>
      <v-card-text>{{ catname }}</v-card-text>
      <v-card-actions>
        <v-btn class="primary">Погладить</v-btn>
      </v-card-actions>
    </v-card>

    <v-card class="ma-5 pa-5">
      <v-text-field label="Имя кота" type="text" v-model="catname" />
    </v-card>
    <v-container>
      <v-row>
        <v-col v-for="(cat, index) in cats" :key="index" cols="12" md="6">
          <v-card class="purple yellow--text">
            <v-card-title>
              {{ cat.name }}
            </v-card-title>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      catname: "Мурзик",
      cats: [
        { name: "Мурзик", breed: "Манул", weight: 10, isAngry: true },
        { name: "Рамзес", breed: "Сфинкс", weight: 2, isAngry: true },
        { name: "Эдуард", breed: "Британец", weight: 5, isAngry: false },
      ],
    };
  },
};
</script>
