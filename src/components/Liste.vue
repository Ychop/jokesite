<template>
  <div>
    <h1>Alle Witze:</h1>
    <ul>
      <li v-for="jokes in joke" :key="jokes.id" class="joke">
        <p
          class="title"
          v-if="jokes.title === 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'"
        >
          <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">( ͡• ͜ʖ ͡• )</a>
        </p>
        <p class="title" v-else>{{ jokes.title }}</p>
        <v-card dense flat id="card">
          <v-card-actions>
            <v-rating v-model="jokes.rating" dense half-increments readonly>
            </v-rating>
            <v-spacer></v-spacer>
            <v-btn
              icon
              id="removebtn"
              @click="remove(jokes.id)"
              v-bind:rmId="jokes.id"
              ><v-icon>mdi-sticker-remove-outline</v-icon></v-btn
            >
          </v-card-actions>
        </v-card>
        <p>{{ jokes.text }} (Id:{{ jokes.id }})</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Liste",
  props: ["joke"],

  methods: {
    remove: function(id) {
      this.$emit("removeEntry", { id: id });
    },
  },
};
</script>

<style scoped>
#removebtn {
  color: red;
}
#card {
  margin-right: 1%;
  background-color: thistle;
}
.joke {
  margin-bottom: 10px;
}
.joke .title {
  font-weight: bold;
  text-decoration-line: underline;
}
ul {
  max-height: 77vh;
  overflow-y: scroll;
}
div {
  max-height: 10vh;
}
</style>
