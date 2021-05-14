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

    <v-form class="ma-5 pa-5" ref="addForm" v-model="formIsValid">
      <v-text-field
        label="Имя кота"
        type="text"
        v-model="newCat.name"
        :rules="formValidation.name"
        required
      />
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
        :rules="formValidation.weight"
      />
      <v-switch v-model="newCat.isAngry" label="Сердит"></v-switch>
      <v-btn class="primary" @click="addCat(newCat)" :disabled="!formIsValid"
        >Добавить</v-btn
      >

      <v-btn color="error" class="ma-4" @click="resetForm()">Сброс формы</v-btn>

      <v-btn color="success" class="ma-4" @click="resetValidation()">
        Сброс валидации
      </v-btn>

      <v-btn color="error" class="ma-4" @click="forceValidation()">
        Принудительная валидация
      </v-btn>

      <v-switch
        v-model="isDarkTheme"
        label="Темная тема"
        @change="changeTheme()"
      ></v-switch>
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
      formValidation: {
        name: [(value) => !!value || "У каждого кота должно быть имя"],
        weight: [
          (value) => !!value || "У каждого кота должен быть вес",
          (value) => value < 15 || "Коты такие толстые не бывают",
        ],
        email: [
          (value) =>
            value.indexOf("@") !== 0 || "Email should have a username.",
          (value) => value.includes("@") || "Email should include an @ symbol.",
          (value) =>
            value.indexOf(".") - value.indexOf("@") > 1 ||
            "Email should contain a valid domain.",
          (value) =>
            value.includes(".") || "Email should include a period symbol.",
          (value) =>
            value.indexOf(".") <= value.length - 3 ||
            "Email should contain a valid domain extension.",
        ],
      },
      formIsValid: false,
      isDarkTheme: false,
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

    resetForm() {
      this.$refs.addForm.reset();
    },
    resetValidation() {
      this.$refs.addForm.resetValidation();
    },
    forceValidation() {
      this.$refs.addForm.validate();
    },
    changeTheme() {
      this.$vuetify.theme.dark = this.isDarkTheme;
    },
  },
};
</script>
