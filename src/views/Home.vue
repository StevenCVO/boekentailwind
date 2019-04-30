<template>
  <div>
    <img
      class="w-1/5 mx-auto mb-8"
      src="@/assets/images/boeken.jpg"
      alt="Afbeelding boeken"
    />
    <data-tabel titel="Boekbeheer" :items="boeken" :kolommen="kolommen">
      <template v-slot:titel-knop>
        <button class="border-2 rounded p-2 hover:bg-blue-600">
          Nieuw boek
        </button>
      </template>
    </data-tabel>
  </div>
</template>

<script>
import axios from "axios";
import DataTabel from "@/components/DataTabel.vue";

export default {
  name: "home",
  components: {
    DataTabel
  },
  data() {
    return {
      boeken: [],
      kolommen: [
        {
          naam: "Titel",
          veld: "titel"
        },
        {
          naam: "Auteur",
          veld: "auteur.naam"
        },
        {
          naam: "Aantal Pagina's",
          veld: "aantalPaginas"
        }
      ]
    };
  },
  async created() {
    // Data ophalen van server
    const boeken = await axios("http://localhost:7000/boeken");
    this.boeken = boeken.data;
  }
};
</script>
