<template>
  <div class="container">
    <div class="header">
      <h1>GOLIVING</h1>
    </div>

    <div class="listBox">
      <h2 class="sub-title">Applications</h2>
      <li class="headers title">
        <span>Name</span>
        <span>Move-in Date</span>
        <span>Requested Room</span>
      </li>
      <div class="list">
        <li
          class="singleUser"
          v-for="entry in databaseEntries"
          :key="entry._id"
        >
          <p>{{ entry.name }}</p>
          <p>{{ entry.date }}</p>
          <p>{{ entry.room }}</p>
        </li>
      </div>
      <div class="bottom">
        <span>Sort by:</span>
        <input @click="alphabeticalSort" type="radio" name="sorter" /> Name
        <input @click="dateSort" type="radio" name="sorter" />
        Date
        <input @click="roomSort" type="radio" name="sorter" />
        Room
        <span class="updateButton" @click="getTheData">Update</span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      databaseEntries: {}
    };
  },
  methods: {
    getTheData() {
      return new Promise((res, rej) => {
        axios.get("http://goliving-api.herokuapp.com/retrieve").then(resp => {
          this.databaseEntries = resp.data;
          res();
        });
      });
    },
    alphabeticalSort() {
      function compare(a, b) {
        const nameA = a.name.toUpperCase();
        const nameB = b.name.toUpperCase();

        let comparison = 0;
        if (nameA > nameB) {
          comparison = 1;
        } else if (nameA < nameB) {
          comparison = -1;
        }
        return comparison;
      }

      this.databaseEntries.sort(compare);
    },
    dateSort() {
      function compare(a, b) {
        const nameA = a.date;
        const nameB = b.date;

        let comparison = 0;
        if (nameA > nameB) {
          comparison = 1;
        } else if (nameA < nameB) {
          comparison = -1;
        }
        return comparison;
      }

      this.databaseEntries.sort(compare);
    },
    roomSort() {
      function compare(a, b) {
        const roomA = a.room;
        const roomB = b.room;

        let comparison = 0;
        if (roomA > roomB) {
          comparison = 1;
        } else if (roomA < roomB) {
          comparison = -1;
        }
        return comparison;
      }

      this.databaseEntries.sort(compare);
    }
  },
  beforeMount() {
    setInterval;
    this.getTheData();
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

.header {
  position: absolute;
  top: 0;
  left: 0;
  height: 50px;
  width: 100%;
  border-bottom: #f4745d solid;
}
h1 {
  position: relative;
  color: #f4745d;
  font-family: "Lato", sans-serif;
  left: 3%;
  width: 20%;
  bottom: 30%;
  letter-spacing: 3.5px;
}
.sub-title {
  background-color: white;
  color: #f4745d;
  width: 100%;
  font-family: "Lato", sans-serif;
  letter-spacing: 1.5px;
  position: relative;
  height: 7.5vh;
  text-align: center;
}
.headers {
  color: white;
  height: 4vh;
  font-family: "Lato", sans-serif;
  display: grid;
  grid-template-areas: "1 2 3";
  grid-template-columns: 25% 47.5% 22.5%;
  font-size: 1.1rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-align: center;
}

.list {
  border-radius: 5px;
  padding: 1%;
  height: 60vh;
  display: grid;
  grid-template-columns: 100%;
  grid-auto-rows: 7.5vh;
  overflow: auto;
}
.singleUser {
  background-color: white;
  font-family: "Lato", sans-serif;
  display: grid;
  grid-template-columns: 32% 37% 28%;
  text-align: left;
}
p {
  position: relative;
  margin-left: 30%;
  font-weight: 600;
}
.listBox {
  position: relative;
  top: 7.5vh;
  border-radius: 10px;
  margin: 0 15% 0 15%;
  height: 85vh;
  overflow: none;
  background: #f4745d;
}
.bottom {
  width: 100%;
  margin-left: 2%;
  margin-top: 1%;
  color: white;
  font-family: "Lato", sans-serif;
}
.updateButton {
  cursor: pointer;
  background-color: white;
  color: #f4745d;
  font-family: "Lato", sans-serif;
  font-weight: 600;
  padding: 5px;
  border-radius: 5px;
  position: relative;
  float: right;
  right: 5%;
}
.updateButton:hover {
  color: white;
  background-color: #f4745d;
  outline: 2px solid white;
}
</style>
