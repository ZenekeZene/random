<template>
  <article class="mini-avatar">
    <section class="image">
      <img
        src="node_modules/frontend-orama-ui/lib/images/boy.gif"
        :alt="`Avatar de ${name}`"
      />
    </section>
    <p class="points">
      Has acertado {{ points }} pregunta {{ points > 1 ? "s" : "" }} en
      <span class="time">5:12</span> minutos. Lo que te da:
      <span class="points__value">65</span> puntos. <br />Eres todo un
      <span>{{ level }}</span
      >.
    </p>
    <base-button class="share" v-ripple simple color-secondary
      >Compartir resultado</base-button
    >
  </article>
</template>
<script>
import { mapState } from "vuex";
export default {
  name: "MiniAvatar",
  props: {
    name: {
      type: String,
      default: "Aureliano Buendía"
    },
    level: {
      type: String,
      default: ""
    }
  },
  computed: {
    ...mapState(["points"])
  }
};
</script>
<style lang="scss" scoped>
.mini-avatar {
  position: relative;

  img {
    float: left;
    height: 5rem;
    margin-top: 0.2rem;
    margin-right: 1rem;
    border-radius: 7px;
  }

  .points {
    margin-bottom: 1rem;
    font-size: 1rem;

    &__value {
      font-size: 1.5rem;
    }
  }

  .aka {
    position: static;
    float: right;
    display: inline-block;
    margin-top: 0.2rem;
    margin-bottom: 0.5rem;
  }

  .share {
    margin-top: 1rem;
    margin-bottom: 1rem;
  }
}
</style>
