<script setup lang="ts">
import { ref, computed } from "vue";
import mon from "@/assets/mon.svg";
import tue from "@/assets/tue.svg";
import wed from "@/assets/wed.svg";
import thu from "@/assets/thu.svg";
import fri from "@/assets/fri.svg";
import sat from "@/assets/sat.svg";
import sun from "@/assets/sun.svg";

const props = defineProps<{
  day: string;
  title: string;
  description?: string;
  offline?: boolean;
  date?: string;
}>();

const streamDate = ref(new Date(props.date ?? 0));

const kanjiDay = computed(() => {
  switch (props.day) {
    case "mon":
      return mon;
    case "tue":
      return tue;
    case "wed":
      return wed;
    case "thu":
      return thu;
    case "fri":
      return fri;
    case "sat":
      return sat;
    default:
      return sun;
  }
});

const startingHourGMT = computed(() => {
  return streamDate.value.toLocaleTimeString("fr-FR", {
    timeZone: "GMT",
    timeStyle: "short",
    hour12: false,
  });
});
const startingHourEST = computed(() => {
  return streamDate.value.toLocaleTimeString("en-US", {
    timeZone: "America/Panama",
    timeStyle: "short",
    hour12: false,
  });
});
const startingHourPST = computed(() => {
  return streamDate.value.toLocaleTimeString("en-US", {
    timeZone: "America/Los_Angeles",
    hour12: false,
    timeStyle: "short",
  });
});
</script>

<template>
  <article class="day-label offline" v-if="offline">
    <div class="day">
      <img :src="kanjiDay" alt="kanji of the day" />
      <div>{{ day }}</div>
    </div>

    <div class="stream-info">
      <div class="title">Information</div>
      <div class="description">// System is in rest mode</div>
    </div>

    <div class="offline-title">Offline</div>

    <div class="reason">Working off stream</div>
  </article>

  <article class="day-label online" v-else>
    <div class="day">
      <img :src="kanjiDay" alt="" />
      <span>{{ day }}</span>
    </div>

    <div class="stream-info">
      <div class="title">{{ title }}</div>
      <div class="description">
        <span class="blank-space"></span>{{ description }}
      </div>
    </div>

    <div class="time-info">
      <ul class="starting-hours">
        <li><span>GMT</span> {{ startingHourGMT }}</li>
        <li><span>EST</span> {{ startingHourEST }}</li>
        <li><span>PST</span> {{ startingHourPST }}</li>
      </ul>
    </div>
  </article>
</template>

<style scoped lang="scss">
.day-label {
  position: relative;
  border: 1px solid rgb(65, 63, 86);
  border-left: 0;
  height: 10%;
  background-color: rgb(30, 20, 60);
  display: flex;
  justify-content: space-between;
  align-items: center;

  &::before {
    content: " ";
    position: absolute;
    display: block;
    top: 0px;
    bottom: 0px;
    left: 0px;
    width: 130px;
    border-style: solid;
    border-width: 48px 48px 48px 80px;
    border-color: transparent transparent transparent rgba(0, 0, 0, 0.538);
  }
  &.offline {
    background-color: rgb(20, 20, 30);

    .stream-info {
      width: auto;

      .title {
        font-family: "Roboto Mono", monospace;
        font-style: normal;
        font-size: 0.8em;
        letter-spacing: 0.2em;
        color: rgb(185, 85, 160);
      }

      .description {
        font-style: italic;
      }
    }

    .offline-title {
      position: relative;
      width: 15%;
      text-align: center;
      font-style: italic;
      font-weight: 700;
      letter-spacing: 0.2em;
      &::before {
        content: "◀";
        position: absolute;
        display: block;
        font-style: normal;
        top: 3px;
        left: -20px;
        font-size: 10px;
      }
      &::after {
        content: "⊽";
        position: absolute;
        display: block;
        font-style: normal;
        top: 0px;
        right: -8px;
        font-size: 15px;
        line-height: 15px;
      }
    }

    .reason {
      position: relative;
      margin-right: -10px;
      padding: 5px 0;
      width: 35%;
      border: 1px solid rgb(105, 100, 125);
      background-color: rgb(36, 30, 66, 50%);
      text-align: center;
      text-transform: none;
      font-size: 0.8em;
      &::after {
        content: "";
        display: block;
        position: absolute;
        top: 9px;
        left: -20px;
        height: 8px;
        width: 22px;
        background-color: white;
        box-shadow: 0px 0px 20px 4px rgba(255, 255, 255, 0.2);
      }
      &::before {
        content: "▶";
        display: block;
        position: absolute;
        top: 10px;
        left: 5px;
        width: 8px;
        height: 8px;
        font-size: 11px;
        line-height: 8px;
        box-shadow: 0px 0px 20px 4px rgba(255, 255, 255, 0.2);
      }
    }
  }

  &.online {
    &::after {
      content: "▶▶▶";
      position: absolute;
      display: block;
      bottom: -15px;
      right: 170px;
      line-height: 35px;
      font-family: "Roboto Mono", monospace;
      font-style: normal;
      font-size: 1.5em;
      letter-spacing: 10px;
      color: rgb(188, 119, 171);
    }
  }
  .day {
    position: relative;
    width: 42px;
    margin-left: 60px;
    font-weight: 700;
    letter-spacing: 0.2em;
    text-align: right;

    img {
      position: absolute;
      width: 130px;
      height: 130px;
      top: -75px;
      left: -70px;
      opacity: 50%;
    }
  }

  .stream-info {
    width: 60%;

    .title {
      font-style: italic;
      font-size: 1.7em;
      font-weight: 700;
    }

    .description {
      display: flex;
      align-items: center;
      font-size: 0.8em;

      .blank-space {
        margin-right: 10px;
        height: 3px;
        width: 70px;
        background-color: white;
      }
    }
  }

  .time-info {
    height: 100%;
    width: 90px;
    margin-top: auto;
    margin-right: 25px;
    border-top: 3px solid rgb(185, 85, 160);
    display: flex;
    align-items: center;
    justify-content: center;
    ul {
      padding: 0;
      list-style-type: none;
      text-align: center;
      li {
        font-family: "Roboto Mono", monospace;
        font-style: normal;
        font-weight: 800;
        font-size: 0.85em;
        display: inline-block;
        line-height: 1.4em;
        span {
          letter-spacing: 0.3em;
          opacity: 1;
        }
      }

      li:nth-child(1) span {
        color: rgb(240, 235, 210);
      }
      li:nth-child(2) span {
        color: rgb(195, 170, 225);
      }
      li:nth-child(3) span {
        color: rgb(195, 150, 180);
      }
    }
  }
}
</style>
