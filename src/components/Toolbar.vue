<template>
  <div>
    <v-toolbar dark id="toolbar">
      <v-text-field label="Suche nach Titel..." v-model="searchtext" dense></v-text-field>
      <v-btn icon @click="search"><v-icon>mdi-magnify</v-icon></v-btn>
      <v-tooltip left>
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on" @click="addnewJoke"
            ><v-icon>mdi-plus</v-icon></v-btn
          >
        </template>
        <span>Erstelle einen Witz</span>
      </v-tooltip>
    </v-toolbar>
    <v-card id="sort" rounded>
      <v-card-actions
        >Sortieren nach:
        <v-spacer></v-spacer>
        <v-btn @click="SortByRating" text>Bewertung</v-btn>
        <v-btn @click="SortById" id="ID" text>ID</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      searchtext: "",
    };
  },
  methods: {
       search: function() {
      if(this.searchtext != ""){
    this.$emit("searching", this.searchtext);
      this.searchtext = "";
      }
    },
    addnewJoke: function() {
      this.$emit("addJoke", {});
    },

    SortByRating: function() {
      this.$emit("sortByRating", {});
    },
    SortById: function() {
      this.$emit("sortById", {});
    },
  },
};
</script>

<style scoped>
#sort {
  background-color: khaki;
}
#ID {
  margin-right: 1%;
}
template {
  max-height: 100%;
  overflow: hidden;
}
</style>
