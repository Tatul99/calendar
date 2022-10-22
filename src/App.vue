<template>
  <div class="main">
    <div class="container">
      <div class="month">
        <p class="title">Select a date</p>
        <div class="icons-m">
          <div class="left" @click="minus(), chengeMonth(), log()"></div>
          <p class="mon">{{ months[getMonth] }}</p>
          <div class="right" @click="plus(), chengeMonth(), log()"></div>
        </div>
      </div>
      <div>
        <div class="content">
          <div v-for="item in days" :key="item" class="days">{{ item }}</div>
        </div>
        <div class="content2">
          <div class="row items" v-for="item2 in days2" :key="item2">
            {{ item2.day }}
          </div>
        </div>
      </div>
      <div class="date">
        <div class="date1">
          {{ day + " " + months[getMonth] + " " + getYear }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  mounted() {
    this.chengeMonth();
    this.log();
  },
  data() {
    return {
      year: new Date().getFullYear(),
      month: new Date().getMonth(),
      dateYear: "",
      day: 9,
      days2: [],
      days: ["Mon", "tue", "Wed", "Thu", "Fri", "Sat", "sun"],
      months: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
    };
  },
  computed: {
    getDate() {
      return new Date(this.year, this.month);
    },
    getDate2() {
      return new Date(this.year, this.month + 1);
    },
    getDate3() {
      return new Date(this.year, this.month - 1);
    },
    getMonth() {
      return new Date(this.year, this.month).getMonth();
    },
    getDay() {
      return new Date(this.year, this.month, this.day).getDay();
    },

    getYear() {
      return new Date(this.year, this.month, this.day).getFullYear();
    },
    daysInMounth() {
      return (this.getDate2 - this.getDate) / 1000 / 3600 / 24;
    },
    getNewDate() {
      return this.getDay;
    },
    dateForNext() {
      return new Date(this.getYear, this.getMonth + 1).getDay();
    },
  },
  methods: {
    plus() {
      this.month++;
    },
    minus() {
      this.month--;
    },
    chengeMonth() {
      this.dateYear = (this.getDate2 - this.getDate) / 1000 / 3600 / 24;
    },

    log() {
      let newdays2 = [];

      for (
        let i = this.getDate.getDay() == 0 ? 5 : this.getDate.getDay() - 2;
        i >= 0;
        i--
      ) {
        let daysInlast = Math.round(
          (this.getDate - this.getDate3) / 1000 / 3600 / 24
        );
        newdays2.push({ day: daysInlast - i, active: false });
      }
      console.log(this.dateYear);
      for (let i = 1; i < this.dateYear + 1; i++) {
        newdays2.push({ day: i, active: true });
      }
      console.log(this.dateForNext);
      for (let i = 1; i <= 7 - this.dateForNext + 1; i++) {
        newdays2.push({ day: i, active: false });
      }

      this.days2 = newdays2;
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
.main {
  padding: 0;
  margin: 0;
  width: 100vw;
  min-height: 100vh;
  background-image: linear-gradient(
    to bottom right,
    rgba(31, 101, 122, 0.7),
    rgb(46, 35, 199, 0.1),
    rgba(93, 25, 148, 0.2),
    rgba(12, 98, 104, 0.4)
  );
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  width: 900px;
  height: 800px;
  background: rgba(63, 133, 190, 0.8);
  border-top-left-radius: 10%;
  border-top-right-radius: 10%;
  opacity: 0.5;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.month {
  width: 100%;
  height: 20%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.title {
  margin-left: 30px;
  font-size: 45px;
  color: aliceblue;
  font-weight: bold;
}
.icons-m {
  width: 200px;
  margin-right: 140px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
.left {
  width: 24px;
  height: 24px;
  -webkit-mask-image: url("../left.png");
  mask-image: url("../left.png");
  -webkit-mask-size: 100%;
  mask-size: 100%;
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;
  background-color: aliceblue;
  cursor: pointer;
}
.right {
  width: 24px;
  height: 24px;
  -webkit-mask-image: url("../right.png");
  mask-image: url("../right.png");
  -webkit-mask-size: 100%;
  mask-size: 100%;
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;
  background-color: aliceblue;
  cursor: pointer;
}
.mon {
  font-size: 30px;
  font-weight: bold;
  color: aliceblue;
}
.date {
  width: 100%;
  height: 20%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.date1 {
  font-size: 30px;
  color: aliceblue;
  font-weight: bold;
}
.content {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(7, auto);
}
.days {
  display: flex;
  justify-content: center;
  font-size: 24px;
  color: aliceblue;
  font-weight: bold;
}
.content2 {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(7, auto);
}
.items {
  display: flex;
  justify-content: center;
  font-size: 24px;
  color: aliceblue;
  font-weight: bold;
}
</style>
