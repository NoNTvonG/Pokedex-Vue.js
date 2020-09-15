<template>
  <div class="footer">
    <div class="container">
      <div class="footer-wrapper">
        <span>&copy; Copyright 2020-{{ date }} by TvonG</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: "",
    };
  },
  methods: {
    dateNow: function() {
      const today = new Date();
      const year = today.getFullYear();
      this.date = year;
    },
  },
  created() {
    setInterval(this.dateNow, 1000);
  },
};
</script>

<style lang="scss" scoped>
.footer {
  min-height: 75px;
  background-color: $alizarin;
  display: flex;
  align-items: center;
  justify-content: center;
  .footer-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    color: $clouds;
  }
}
</style>
