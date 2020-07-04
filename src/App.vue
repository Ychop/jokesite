<template>
  <v-app id="app">
    <Toolbar
      id="tools"
      @addJoke="changeShow"
      @searching="searchJoke"
      @sortByRating="sortByRating"
      @sortById="sortById"
    ></Toolbar>
    <Suche
      :searchtext="searchText"
      :hitList="hitlist"
      v-show="showSearch"
      @removeEntry="removeEntry"
      @backToMainPage="changeShow"
    ></Suche>
    <Liste
      :joke="list"
      v-show="showJokePage"
      @removeEntry="removeEntry"
    ></Liste>
    <Witzerstellen
      :jokes="list"
      v-show="showCreatePage"
      @abort="changeShow"
      @Add="addEntry"
    ></Witzerstellen>
  </v-app>
</template>

<script>
import axios from "axios";
import Toolbar from "./components/Toolbar.vue";
import Liste from "./components/Liste.vue";
import Witzerstellen from "./components/Witzerstellen.vue";
import Suche from "./components/Suche.vue";

export default {
  name: "App",

  components: {
    Toolbar,
    Liste,
    Suche,
    Witzerstellen,
  },

  data: () => {
    return {
      list: [],
      searchText: "",
      showCreatePage: false,
      showSearch: false,
      showJokePage: true,
      reverse: 1,
    };
  },

  methods: {
    searchJoke: function(e) {
      this.searchText = e;
      if (this.showSearch === false) {
        this.showSearch = true;
        this.showJokePage = false;
      }
    },

    sortById: function() {
      if (this.reverse == 1) {
        this.reverse = 0;
        return this.list.sort((a, b) => {
          return a.id - b.id;
        });
      } else {
        this.reverse = 1;
        return this.list.sort((a, b) => {
          return b.id - a.id;
        });
      }
    },
    sortByRating: function() {
      if (this.reverse == 1) {
        this.reverse = 0;
        return this.list.sort((a, b) => {
          return b.rating - a.rating;
        });
      } else {
        this.reverse = 1;
        return this.list.sort((a, b) => {
          return a.rating - b.rating;
        });
      }
    },

    removeEntry: function(e) {
      axios
        .delete("https://jokesiteserver.herokuapp.com/jokes/" + e.id)
        .then((response) => {
          this.list = response.data;
        });
    },
    changeShow: function() {
      if (this.showCreatePage === true || this.showSearch === true) {
        this.showCreatePage = false;
        this.showSearch = false;
        this.showJokePage = true;
      } else if (this.showSearch === true || this.showJokePage === true) {
        this.showCreatePage = true;
        this.showSearch = false;
        this.showJokePage = false;
      }else if (this.showCreatePage === true || this.showJokePage === true) {
        this.showCreatePage = false;
        this.showSearch = true;
        this.showJokePage = false;
      }
    },
    addEntry: function(e) {
      axios
        .post("https://jokesiteserver.herokuapp.com/jokes", {
          rating: e.rating,
          title: e.title,
          text: e.text,
          id: e.id,
        })
        .then((response) => {
          this.list = response.data;
        });

      this.showCreatePage = false;
      this.showJokePage = true;
    },
  },
  computed: {
    hitlist() {
      if (this.searchText != "") {
        return this.list.filter(({ title }) => {
          return title.toLowerCase().includes(this.searchText.toLowerCase());
        });
      }
    },
  },
  mounted() {
    axios.get("https://jokesiteserver.herokuapp.com/jokes").then((response) => {
      this.list = response.data;
    });
  },
};
</script>

<style>
#app {
  background-color: thistle;
}
</style>
