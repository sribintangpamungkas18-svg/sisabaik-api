<script setup>
import { visualKategori } from "../lib/visual.js";
import Ikon from "./Ikon.vue";

const props = defineProps({
  pencarian: { type: String, required: true },
  kategori: { type: String, required: true },
  daftarKategori: { type: Array, required: true },
});

const emit = defineEmits(["ubah-pencarian", "ubah-kategori", "reset"]);
</script>

<template>
  <form
    class="filter"
    role="search"
    aria-label="Filter katalog makanan"
    @submit.prevent
  >
    <!-- Kolom Pencarian Teks -->
    <div>
      <label for="cari">Cari makanan atau penyedia</label>
      <div class="input-icon">
        <Ikon nama="cari" />
        <input
          id="cari"
          :value="props.pencarian"
          type="search"
          maxlength="100"
          placeholder="Roti, nasi, atau nama usaha…"
          @input="emit('ubah-pencarian', $event.target.value)"
        />
      </div>
    </div>

    <!-- Dropdown Filter Kategori -->
    <div>
      <label for="kategori-filter">Kategori makanan</label>
      <select
        id="kategori-filter"
        :value="props.kategori"
        @change="emit('ubah-kategori', $event.target.value)"
      >
        <option value="">Semua kategori</option>
        <option
          v-for="nilai in props.daftarKategori"
          :key="nilai"
          :value="nilai"
        >
          {{ visualKategori(nilai).label }}
        </option>
      </select>
    </div>

    <!-- Tombol Reset -->
    <button
      class="button-secondary"
      type="button"
      @click="emit('reset')"
    >
      <Ikon nama="ulang" />Reset filter
    </button>
  </form>
</template>