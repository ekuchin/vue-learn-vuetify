<template>
  <div class="about">
    <h1>This is an about page</h1>

    <v-container>
      <v-row>
        <v-col v-for="(cat, index) in cats" :key="index" cols="12" md="6">
          <v-card class="purple yellow--text">
            <v-card-title>
              {{ cat.name }}
            </v-card-title>
            <v-card-subtitle>
              {{ cat.breed }}, вес {{ cat.weight }}кг,
              {{ cat.isAngry ? "Сердит" : "Дружелюбен" }}
            </v-card-subtitle>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <v-form class="ma-5 pa-5">
      <v-text-field label="Имя кота" type="text" v-model="newCat.name" />
      <v-combobox
        v-model="newCat.breed"
        :items="breeds"
        label="Порода"
        clearable
      ></v-combobox>
      <v-text-field
        label="Вес кота"
        type="text"
        v-model.number="newCat.weight"
      />
      <v-switch v-model="newCat.isAngry" label="Сердит"></v-switch>
      <v-btn class="primary" @click="addCat(newCat)">Добавить</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      newCat: {
        name: "Мурзик",
        breed: "Манул",
        weight: 10,
        isAngry: true,
      },
      cats: [
        { name: "Мурзик", breed: "Манул", weight: 10, isAngry: true },
        { name: "Рамзес", breed: "Сфинкс", weight: 2, isAngry: true },
        { name: "Эдуард", breed: "Британец", weight: 5, isAngry: false },
      ],
    };
  },

  computed: {
    breeds: function () {
      return this.cats.map((cat) => {
        return cat.breed;
      });
    },
  },

  methods: {
    addCat: function (cat) {
      const { name, breed, weight, isAngry } = cat;
      this.cats.push({ name, breed, weight, isAngry });
    },
  },
};
</script>
