<template lang="pug">
#highscore
  header.head
    .container.top
      .title
        h1 Teilnehmer
      .nes-field.is-inline.filter
        input#name.nes-input.is-error(type='text', v-model="filter")
  
  .nes-table-responsive
    table.nes-table.is-bordered.is-centered
      thead
        tr
          th Name
          th Plane
          th Alter
          th Punkte
          th 
            nuxt-link.nes-btn.is-success(to="/add/new") +

      tbody
        tr(v-for="(participant,idx) in participants", :key="idx")
          td {{participant.name}}
          td {{participant.plane}}
          td {{participant.age}}
          td {{participant.sum}}
          td
            button.nes-btn.is-primary(@click="edit(participant)") #
            button.nes-btn.is-error(type='button',@click="remove(participant)") -

</template>

<script>
import Participant from '@/components/participant'
export default {
  components: { Participant },
  data() {
    return {
      filter: ''
    }
  },
  pouch: {
    participants: function() {
      if (this.filter == "") {
        console.log('all')
        return {
          database: "participants",
          selector: {},
          sort: [{sum: "desc"}],

        }
      } else {
        console.log('filter', this.filter)
        return {
          database: "participants",
          selector: { name: {$regex: this.filter }},
          sort: [{sum: "desc"}],
        }
      }
    }  
  },
  methods: {
    remove(part) {
      console.log('remove: ', part)
      if (part) this.$pouch.remove("participants", part)
    },
    edit(part) {
      if (part._id) this.$router.push({
        path: `/add/${part._id}`
      })
    }
  },
}
</script>

<style scoped>
.head {
  border-bottom: 8px solid grey;
  grid-area: header;
}
.top {
  display: flex;
  flex-direction: row;
  justify-content: space-between;

}
.filter {
  margin-right: 10px;
}

</style>
