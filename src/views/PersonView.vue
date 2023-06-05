<script>
export default {
  data() {
    return {
      person: {},
      loading: false,
    };
  },
  methods: {
    getPerson(url) {
      this.loading = true;
      fetch(url)
        .then((res) => res.json())
        .then((data) => {
          const { name, birth_year, height, eye_color } = data;
          this.person = {
            Name: name,
            "Birth Year": birth_year,
            Height: height,
            "Eye color": eye_color,
          };
          this.loading = false;
        });
    },
    async getPerson2(url) {
      this.loading = true;
      const res = await fetch(url);
      const data = await res.json();

      const { name, birth_year, height, eye_color } = data;
      this.person = {
        Name: name,
        "Birth Year": birth_year,
        Height: height,
        "Eye color": eye_color,
      };
      this.loading = false;
    },
    goBack() {
      this.$router.push("/")
    }
  },
  mounted() {
    const id = this.$route.params.id;
    this.getPerson(`https://swapi.dev/api/people/${id}`);
    this.getPerson2(`https://swapi.dev/api/people/${id}`);
  },
};
</script>

<template>
  <main>
    <h3 v-show="loading">Carregando...</h3>
    <table v-show="!loading">
      <button @click="goBack" class="voltar">&#60;</button>
      <tr v-for="(value, label) in person" :key="label">
        <th>{{ label }}</th>
        <td>{{ value }}</td>
      </tr>
    </table>
  </main>
</template>

<style scoped>
table {
  position: relative;
}

td {
  padding: 0 1.5rem;
}
th {
  font-weight: 600;
  color: #00ddb3;
}

.voltar {
  position: absolute;
  left: -5rem;
  top: -0.5rem;
  height: 50px;
  width: 50px;
  font-size: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
