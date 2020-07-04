<template>
  <div>
       <p id="noEntry" v-if="hitList.length == 0">Leider wurde kein Titel gefunden </p>
    <ul>
      <li v-for="hits in hitList" :key="hits.id" class="hitlist">
     
        <p class="title">{{ hits.title }}</p>
        <v-card dense flat id="card">
          <v-card-actions>
            <v-rating v-model="hits.rating" dense half-increments readonly>
            </v-rating>
            <v-spacer></v-spacer>
            <v-btn
              icon
              id="removebtn"
              @click="remove(hits.id)"
              v-bind:rmId="hits.id"
              ><v-icon>mdi-sticker-remove-outline</v-icon></v-btn
            >
          </v-card-actions>
        </v-card>
        <p>{{ hits.text }} (Id:{{ hits.id }})</p>
      </li>
    </ul>
    <v-btn id="back" @click="backToMainPage">Zurück zur Startseite</v-btn>
  </div>
</template>

<script>
export default {
  props: ["hitList"],


  methods: {
    remove: function(id) {
      this.$emit("removeEntry", { id: id });
    },
    backToMainPage: function(){
      this.$emit("backToMainPage");
    }
  },

}
</script>

<style>
#noEntry{
  font-weight: bold;
  font-size: 250%;
  margin-top: 1%;
}
#back{
  position: absolute;
  margin-top: 2%;
  right: 3%;
  background-color:khaki;
}
#removebtn {
  color: red;
}
#card {
  margin-right: 1%;
  background-color: thistle;
}
.hitlist {
  margin-bottom: 10px;
}
.hitlist .title {
  font-weight: bold;
  text-decoration-line: underline;
}
ul {
  max-height: 77vh;
  overflow-y: scroll;
}
</style>
