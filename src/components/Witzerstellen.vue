<template>
  <div id="erstellung">
    <h1>Erstelle einen Witz:</h1>
    <v-text-field
      v-model="title"
      placeholder="hier Titel eingeben..."
      label="Titel:"
      class="input"
    ></v-text-field>
    <v-textarea
      v-model="text"
      placeholder="hier den Witz eingeben..."
      label="Text:"
      class="input"
    ></v-textarea>
    <v-card class="card" flat>
      <v-card-actions>
        <p>Bewertung :</p>
        <v-spacer></v-spacer>
        <v-rating half-increments v-model="rating"> </v-rating>
      </v-card-actions>
    </v-card>
    <v-card class="card" flat>
      <v-card-actions>
        <p>Witz Id: {{ this.jokes.length }}</p>
        <v-spacer></v-spacer>
        <v-btn id="btn" @click="abort">Abbrechen</v-btn>
        <v-btn id="btn" @click="add">Hinzufügen</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "Witzerstellen",
  props: ["jokes"],
  data: function() {
    return {
      title: "",
      text: "",
      idcount: 0,
      rating: 0,
    };
  },
  methods: {
    add: function() {
      if (this.title.length < 0 || this.text.length < 0) {
        alert("Fehler beim Hinzufügen Text/Tiel dürfen nicht Leer sein.");
      }
      if (this.title === "Immortal") {
        this.$emit("Add", {
          title: "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
          text: "What could this mean?",
          id: this.jokes.length,
          rating: 5,
        });
      } else {
        this.$emit("Add", {
          title: this.title,
          text: this.text,
          rating: this.rating,
          id: this.jokes.length,
        });
      }
      this.title = "";
      this.text = "";
      this.idcount = this.jokes.length;
      this.rating = 0;
    },
    abort: function() {
      this.$emit("abort", {});
    },
  },
};
</script>

<style scoped>
.input {
  margin-left: 1%;
  margin-right: 1%;
}
.card {
  background-color: thistle;
}
#btn {
  background-color: khaki;
}
</style>
