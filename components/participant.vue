<template lang="pug">
.participant.nes-container.is-dark.member-card(v-if="participant")
  .avatar
    img(:src="url")
  .name
    h2 {{participant.name}}
  .plane
    h3 Flugzeug: {{participant.plane}}
  .points
    .nes-badge
      span(:class="{ 'is-warning': participant.run1 !== max, 'is-success': participant.run1 === max }") 1: {{participant.run1}}cm
    .nes-badge
      span(:class="{ 'is-warning': participant.run2 !== max, 'is-success': participant.run2 === max }") 2: {{participant.run2}}cm
    .nes-badge
      span(:class="{ 'is-warning': participant.run3 !== max, 'is-success': participant.run3 === max }") 3: {{participant.run3}}cm
    .nes-badge
      span.is-primary Design: {{participant.design}}
  .sum
    h1 {{sum}}


</template>

<script>
export default {
  components: {
  },
  props: ["participant"],
  data() {
    return {
      demoparticipant: {
        name: "Emily",
        plane: "SuperFlyer",
        run1: 100,
        run2: 20150,
        run3: 3040,
        design: 80
      }
    }
  },
  computed: {
    url() {
      return `https://api.adorable.io/avatars/100/${this.participant.name}.png`
    },
    sum() {
      const s = this.participant.design + this.max
      return s
    },
    max() {
      return Math.max(this.participant.run1, this.participant.run2, this.participant.run3)
    },
  }
}
</script>

<style>
.participant {
  display: grid;
  grid-gap: 10px;
  grid-template-rows: min-content min-content min-content;
  grid-template-columns: min-content 1fr min-content;
  grid-template-areas: "avatar name sum" "avatar plane sum" "points points points";
  background-color: grey;
}

.avatar {
  grid-area: avatar;
}

.name {
  grid-area: name;
}

.plane {
  grid-area: plane;
}

.points {
  grid-area: points;
  display: flex;
  justify-content: space-between;
}

.sum {
  grid-area: sum;
}

</style>