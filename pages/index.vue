<template lang="pug">
#highscore
  header.head
    .container
      h1 Highscore
  
  .kids.nes-container.with-title
    h3 Kinder (0-12)
    Participant(v-for="participant in kids", :key="participant._id", :participant="participant")

  .youth.nes-container.with-title
    h3 Jugendliche (13-18)
    Participant(v-for="participant in youth", :key="participant._id", :participant="participant")




</template>

<script>
import Participant from '@/components/participant'
export default {
  components: { Participant },
  pouch: {
    participants: {},
    kids: function() {
      return {
        database: 'participants', // you can pass a database string or a pouchdb instance
        selector: {age: { $lt:13 }},
        sort: [{sum: "asc"}],
      }
    },
    youth: function() {
      return {
        database: 'participants', // you can pass a database string or a pouchdb instance
        selector: {age: { $gt:12 }},
        sort: [{sum: "asc"}],
      }
    },
  },
  mounted() {
    console.log(this.participants)
  }
}
</script>

<style scoped>
#highscore {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: min-content 1fr;
  grid-template-areas: "header header" "kids youth";
  grid-gap: 10px;
}

.head {
  border-bottom: 8px solid grey;
  grid-area: header;
}

.kids {
  grid-area: kids;
}

.youth {
  grid-area: youth;
}
</style>
