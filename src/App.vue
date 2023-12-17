<script setup lang="ts">
import DayLabel from "./components/DayLabel.vue";
</script>

<template>
  <main class="next-stream">
    <section class="schedule">
      <DayLabel day="mon" offline title="Working off stream" />
      <DayLabel
        day="tue"
        title="Art Stream"
        description="Doing my third strip game drawing!"
        date="2023-12-15T21:00:00+01:00"
      />
      <DayLabel day="wed" offline title="Working off stream" />
      <DayLabel day="thu" offline title="Working off stream" />
      <DayLabel day="fri" offline title="Working off stream" />
      <DayLabel day="sat" offline title="Working off stream" />
      <DayLabel day="sun" offline title="Working off stream" />
    </section>

    <section class="week-information">
      <div>
        <h2>DEC 11 - DEC 17</h2>
      </div>
      <h1>Schedule</h1>
    </section>
  </main>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Roboto+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap");

html,
body,
#app,
main {
  height: 100%;
}

body {
  margin: 0;
  background-color: rgb(25, 25, 35);
  font-family: "Poppins", sans-serif;
  text-transform: uppercase;
  color: white;
}

.next-stream {
  display: grid;
  grid-template-columns: 10fr repeat(2, 1fr) 10fr;

  .schedule {
    grid-column: 1/4;
    grid-row: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    background: url("@/assets/wallhaven.png") no-repeat right top;
    background-size: cover;
    mask: linear-gradient(to right, white 60%, transparent 100%);
   /* z-index: 1; // fix unwanted transparency on children*/
  }

  .week-information {
    grid-column: 2/6;
    grid-row: 1;
    background: url("@/assets/background.avif") no-repeat right top;
    background-size: cover;
    mask: linear-gradient(to left, white 60%, transparent 100%);
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    flex-direction: column;
  }
}
</style>
