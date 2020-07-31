<template>
  <div v-if="loaded">
    <section
      class="text-3xl flex justify-center content-center flex-col mx-auto text-center"
    >
      <h1 v-if="!expired">Buy Now</h1>
      <h1 v-else>Timer is done</h1>
    </section>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2 relative">
        {{ display_days }}
        <div class="label text-sm absolute bottom-0">days</div>
      </div>
      <span class="leading-strong"> :</span>
      <div class="days mr-2 relative">
        {{ display_hours }}
        <div class="label text-sm absolute bottom-0">hours</div>
      </div>
      <span class="leading-strong"> :</span>
      <div class="days mr-2 relative">
        {{ display_minutes }}
        <div class="label text-sm absolute bottom-0">min</div>
      </div>
      <span class="leading-strong"> :</span>
      <div class="days mr-2 relative">
        {{ display_seconds }}
        <div class="label text-sm absolute bottom-0">seconds</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  props: ["year", "month", "date", "hour", "minute", "second", "millisecond"],
  data: () => ({
    display_days: 0,
    display_hours: 0,
    display_minutes: 0,
    display_seconds: 0,
    loaded: false,
    expired: false,
  }),
  computed: {
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      );
    },
    _seconds: () => 1000,
    _minutes: function() {
      return this._seconds * 60;
    },
    _hours: function() {
      return this._minutes * 60;
    },
    _days: function() {
      return this._hours * 24;
    },
  },
  mounted() {
    this.showTimming();
  },
  methods: {
    formatNum: (num) => (num < 10 ? "0" + num : num),
    showTimming() {
      const timer = setInterval(() => {
        const now = new Date();
        // const end = new Date(2020, 7, 4, 10, 10, 10, 10);
        const distance = this.end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          this.expired = true;
          return;
        }

        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.display_minutes = this.formatNum(minutes);
        this.display_seconds = this.formatNum(seconds);
        this.display_hours = this.formatNum(hours);
        this.display_days = this.formatNum(days);
        this.loaded = true;
      }, 1000);
    },
  },
};
</script>

<style lang="css" scoped></style>
