<template>
  <section>
    <base-card>
      <h2>{{ fullName }}</h2>
      <h3>${{ rate }}/hourly</h3>
    </base-card>
  </section>
  <section>
    <base-card>
      <header>
        <h2>Interested ? Reach Out now</h2>
        <base-button link :to="contactLink">Contact!</base-button>
      </header>
      <router-view></router-view>
    </base-card>
  </section>
  <section>
    <base-card>
      <base-badge
        v-for="area in areas"
        :key="area"
        :type="area"
        :title="area"
      ></base-badge>
      <p>{{ description }}</p>
    </base-card>
  </section>
</template>

<script>
export default {
  props: ['id'],
  date() {
    return {
      selectedCoach: null
    };
  },
  created() {
    this.selectedCoach = this.$store.getters['coaches/coaches'].find(
      coach => coach.id === this.id
    );
  },
  computed: {
    fullName() {
      return this.selectedCoach.firstName + ' ' + this.selectedCoach.lastName;
    },
    rate() {
      return this.selectedCoach.hourlyRate;
    },
    description() {
      return this.selectedCoach.description;
    },
    areas() {
      return this.selectedCoach.areas;
    },

    contactLink() {
      return this.$route.path + '/' + this.id + '/contact';
    }
  }
};
</script>

<style></style>
