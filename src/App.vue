<template>
  <div id="app">
    <h1>Contoh Halaman Web</h1>

    <input type="text" v-model="nama" placeholder="Masukkan Nama Anda" />

    <p
      class="pesan"
      :class="{ besar: ukuranFont === 'besar' }"
      :style="{ color: warna }"
    >
      Halo, {{ nama }}!
    </p>

    <button @click="ubahUkuranFont">Ubah Ukuran Font</button>
    <button @click="ubahWarna">Ubah Warna</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nama: "",
      ukuranFont: "kecil",
      warna: "blue",
    };
  },
  methods: {
    ubahUkuranFont() {
      this.ukuranFont = this.ukuranFont === "besar" ? "kecil" : "besar";
    },
    ubahWarna() {
      this.warna = this.warna === "blue" ? "red" : "blue";
    },
  },
};
</script>

<style scoped>
.pesan {
  font-size: 16px;
}

.pesan.besar {
  font-size: 24px;
}
</style>
