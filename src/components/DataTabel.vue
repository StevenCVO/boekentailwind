<template>
  <table class="w-full">
    <caption class="bg-blue-500 text-white text-xl p-4">
      <div class="flex flex-row justify-between items-center">
        <span class="font-semibold">{{ titel }}</span>
        <slot name="titel-knop"></slot>
      </div>
    </caption>
    <thead>
      <tr>
        <th
          class="text-left p-2 border-b"
          v-for="kolom of kolommen"
          :key="kolom.veld"
        >
          {{ kolom.naam }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr class="border" v-for="item of gepagineerd" :key="item[itemKey]">
        <td class="p-2" v-for="kolom of kolommen" :key="kolom.veld">
          {{ getWaardeViaVeld(item, kolom.veld) }}
        </td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td :colspan="kolommen.length">
          <div class="flex justify-end py-4 px-10 items-center">
            <div class="mx-4">Rijen per pagina</div>
            <select class="mx-4 border-b" v-model="perPagina">
              <option value="5">5</option>
              <option value="10">10</option>
              <option value="15">15</option>
              <option :value="items.length">Alles</option>
            </select>
            <div class="mx-4">
              {{ (huidigePagina - 1) * perPagina + 1 }} -
              {{ Math.min(huidigePagina * perPagina, items.length) }}
              van {{ items.length }}
            </div>
            <i
              :class="{ 'opacity-25': huidigePagina === 1 }"
              class="material-icons cursor-pointer"
              >keyboard_arrow_left</i
            >
            <i class="material-icons cursor-pointer">keyboard_arrow_right</i>
          </div>
        </td>
      </tr>
    </tfoot>
  </table>
</template>

<script>
export default {
  data() {
    return {
      perPagina: 5,
      huidigePagina: 1
    };
  },
  props: {
    titel: {
      type: String,
      default: "Titel"
    },
    items: {
      type: Array,
      // zelfde als:
      // function() {
      //   return []
      // }
      default: () => []
    },
    itemKey: {
      type: String,
      default: "_id"
    },
    kolommen: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    gepagineerd() {
      return this.items.slice(
        (this.huidigePagina - 1) * this.perPagina,
        Math.min(this.huidigePagina * this.perPagina, this.items.length)
      );
    }
  },
  methods: {
    getWaardeViaVeld(obj, veldString) {
      // obj is bv. boek
      // veldString is bv. "auteur.naam"

      // String omzetten naar array van velden
      const veldArray = veldString.split(".");

      // Zoeken in de diepte vanuit het startobject
      return veldArray.reduce((res, veld) => {
        return res[veld];
      }, obj);
    }
  }
};
</script>

<style></style>
