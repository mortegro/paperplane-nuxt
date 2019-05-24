<template lang="pug">
#highscore
  header.head
    .container
      h1 Highscore
  .kids.nes-container.with-title
    h3 Kinder (0-12)
    Participant
    Participant

  .youth.nes-container.with-title
    h3 Jugendliche (13-18)
    Participant



</template>

<script>
import Participant from '@/components/participant'
export default {
  components: { Participant }
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
