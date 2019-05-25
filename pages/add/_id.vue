<template lang="pug">
#add-page(v-on:keyup.enter="alert")
  header.head
    .container
      h1(v-if="!item._id") Teilnehmer anlegen 
      h1(v-else="") {{item.name}} bearbeiten
  .nes-container.with-title
    h3 Teilnehmerdaten
    .nes-field.is-inline
      label(for='name') Name Teilnehmer
      input#name.nes-input.is-error(type='text', v-model="item.name")
    .nes-field.is-inline
      label(for='plane') Name Flieger
      input#plane.nes-input.is-error(type='text', v-model="item.plane")
    .nes-field.is-inline
      label(for='age') Alter (Jahre)
      input#age.nes-input.is-warning(type='text', v-model="item.age")
  .nes-container.with-title
    h3 Daten Flug
    .nes-field.is-inline
      label(for='design') Design
      input#design.nes-input.is-warning(type='text', v-model="item.design")
    .nes-field.is-inline(style="margin-top: 24px;")
      label(for='run1') Flug 1
      input#run1.nes-input.is-success(type='text', v-model="item.run1")
    .nes-field.is-inline
      label(for='run2') Flug 2
      input#run2.nes-input.is-success(type='text', v-model="item.run2")
    .nes-field.is-inline
      label(for='run3') Flug 3
      input#run3.nes-input.is-success(type='text', v-model="item.run3")
  .nes-container#buttons
    button.nes-btn.is-success(type='button',@click="save") Speichern
    button.nes-btn.is-warning(type='button',@click="cancel") Cancel


</template>

<script>
  export default {
    data: () => ({
      id: null,
      item:{}
    }),
    pouch: {
      item: function() {
        return {
          database: "participants",
          selector: {_id: this.$route.params.id},
          first: true
        }
      }  
    },
    methods: {
      save() {
        const item = this.sanitize(this.item)
        if (item && item.name && item.age) {
          if (!item._id) {
            // Create
            console.log('creating:', item)
            this.$pouch.post("participants",{...item})
            this.cancel()
          } else {
            // Update
            console.log('updating:',item)
            this.$pouch.put("participants",{...item},{})
            this.cancel()
          }
        }
      },
      cancel() {
        this.item = {}
        this.id= null
        this.$router.push({path: '/list'})

      },
      sanitize(item) {
        item.age = parseInt(item.age, 10)
        item.run1 = parseInt(item.run1, 10)
        item.run2 = parseInt(item.run2, 10)
        item.run3 = parseInt(item.run3, 10)
        item.design = parseInt(item.design, 10)
        item.sum = Math.max(item.run1, item.run2, item.run3) + item.design || 0
        
        return item
      },
      alert() {
        this.save()
      }
    },
  }
</script>

<style scoped>
#add-page {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: min-content 1fr;
  grid-template-areas: "header" "add";
  grid-gap: 10px;
}

.head {
  border-bottom: 8px solid grey;
  grid-area: header;
}

.nes-field {
  margin-top: 8px;
}

.add {
  grid-area: add;
}

#buttons {
  display: flex;
  justify-content: space-around;
  padding-top: 12px;
}

</style>
