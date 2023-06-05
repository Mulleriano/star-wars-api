<script>
export default {
  data() {
    return {
      people: [],
      loading: false,
      nextPeople: null,
      prevPeople: null,
    };
  },
  methods: {
    getPeople(url) {
      this.loading = true;
      fetch(url)
        .then((res) => res.json())
        .then((data) => {
          this.people = data.results;
          this.nextPeople = data.next;
          this.prevPeople = data.previous;
          this.loading = false;
        });
    },
    prev() {
      this.getPeople(this.prevPeople);
    },
    next() {
      this.getPeople(this.nextPeople);
    },
  },
  mounted() {
    this.getPeople("https://swapi.dev/api/people/");
  },
};
</script>

<template>
  <main>
    <h3 v-show="loading">Carregando...</h3>

    <table v-show="!loading">
      <tr>
        <th>Name</th>
        <th>Gender</th>
        <th>Height</th>
      </tr>
      <tr v-for="person in people" :key="person.name">
        <td class="label">
          <RouterLink :to="`/people/${person.url.split('/')[5]}`">
            {{ person.name }}
          </RouterLink>
        </td>
        <td>{{ person.gender }}</td>
        <td>{{ person.height }}</td>
      </tr>
    </table>

    <div v-show="!loading" id="container">
      <button @click="prev">prev</button>
      <button @click="next">next</button>
    </div>
  </main>
</template>

<style scoped>
.label {
  text-align: left;
}
</style>
