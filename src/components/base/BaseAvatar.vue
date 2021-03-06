<template>
  <article class="avatar">
    <span class="logout" v-mobile-hover:#4992a9
      ><span class="icon-log-out"></span
    ></span>
    <section>
      <h2 v-if="withGreetings">{{ getGreetings }}</h2>
      <section class="image">
        <img :src="user.photoURL" :alt="`Avatar de ${user.name}`" />
        <div class="info">
          <span class="aka">{{ level }}</span>
          <p class="points" m-b-0>
            Record:
            <span class="points__value">65</span> puntos.
          </p>
        </div>
      </section>
      <base-button class="share" v-ripple color-secondary
        >Compartir</base-button
      >
      <slot></slot>
    </section>
  </article>
</template>
<script>
import * as moment from "moment";
import { mapState } from "vuex";

export default {
  name: "Avatar",
  props: {
    name: {
      type: String,
      default: "Aureliano Buendía"
    },
    level: {
      type: String,
      default: ""
    },
    withGreetings: {
      type: Boolean,
      default: true
    },
    userName: {
      type: String,
      default: ""
    }
  },
  computed: {
    ...mapState("user", ["user"]),
    getGreetings() {
      return `${this.getGreetingTime(moment())}, ${this.user.name}.`;
    }
  },
  methods: {
    getGreetingTime: currentTime => {
      if (!currentTime || !currentTime.isValid()) {
        return "Hello";
      }

      const splitAfternoon = 12; // 24hr time to split the afternoon
      const splitEvening = 21; // 24hr time to split the evening
      const currentHour = parseFloat(currentTime.format("HH"));

      if (currentHour >= splitAfternoon && currentHour <= splitEvening) {
        // Between 12 PM and 5PM
        return "Buenas tardes";
      } else if (currentHour >= splitEvening) {
        // Between 5PM and Midnight
        return "Buenas noches";
      }
      // Between dawn and noon
      return "Buenos días";
    }
  }
};
</script>
<style lang="scss" scoped>
.logout {
  position: absolute;
  top: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 4rem;
  height: 2rem;
  margin: 0;
  padding-top: 1rem;
  padding-right: 0.5rem;
  font-size: 1.2rem;
  color: white;
  text-align: center;
}

.avatar {
  padding: 0.5rem 1rem 1rem 1rem;

  > * {
    margin-bottom: 1rem;

    &:last-child {
      margin-bottom: 0;
    }
  }

  h2 {
    padding-right: 3rem;
    font-size: 1.2rem;
  }
}

.info {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  flex-grow: 1;
  padding: 0 0.5rem 0.5rem 1rem;
}

.image {
  position: relative;
  display: flex;
  align-items: flex-start;
  margin-bottom: 0;

  img {
    width: 70px;
    height: auto;
    display: block;
    border-radius: 0.5rem;
  }
}

.points {
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
  font-size: 1rem;

  &__value {
    color: var(--color-tertiary);
  }
}

.share {
  margin-top: 1rem;
  margin-bottom: 0;
}
</style>
