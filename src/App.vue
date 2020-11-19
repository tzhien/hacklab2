<template>
  <div id="app">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <b-col> </b-col>

    <b-row>
      <!--<button type="button" v-on:click="filterByTo('doctor')" class="zi-2">
        Get Doctor
      </button>-->
      <b-container class="main-container" fluid>
        <img src="./assets/web layout-02.png" />
        <!-- <div class="parallax"></div> -->

        <form @submit.stop.prevent="submit">
          <div class="title">
            <h2>THE COVID HERO</h2>
          </div>

          <div class="formword">
            <label for="fname">Name</label>
            <input
              type="text"
              id="fname"
              name="firstname"
              v-model="firstname"
              placeholder="Your name"
            />

            <label for="lname">Messages</label>
            <input
              type="text"
              id="message"
              name="message"
              v-model="message"
              placeholder="Leave your message"
            />

            <label for="country">To</label>
            <select id="to" name="To" v-model="to">
              <option value="doctor">Doctor</option>
              <option value="nurse">Nurse</option>
              <option value="army">Army</option>
              <option value="police">Police</option>
            </select>
          </div>

          <div class="button mb-2">
            <!-- <b-button @click="showMsgBoxOne">Simple msgBoxOk</b-button> -->
            <input type="submit" value="SUBMIT" @click="showMsgBoxOne" />
          </div>

          <div class="button2">
            <a href="https://codepen.io/Abby98/full/NWrVrgO" class="button2"
              >VIEW</a
            >
            <a href="https://codepen.io/zhien/full/abZXepa" class="button3"
              >INFO</a
            >
          </div>

          <!-- <div class="button3">
            <a :href="'https://codepen.io/zhien/full/abZXepa'">INFO</a>
          </div> -->
        </form>
      </b-container>
    </b-row>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      boxOne: "",
      boxTwo: "",
      firstname: "",
      message: "",
      to: "",
    };
  },

  methods: {
    showMsgBoxOne() {
      this.boxOne = "";
      this.$bvModal
        .msgBoxOk("Thanks for your submission")
        .then((value) => {
          this.boxOne = value;
        })
        .catch((err) => {
          // An error occurred
        });
    },

    submit() {
      //if you want to send any data into server before redirection then you can do it here
      axios
        .get(
          `https://filechats.herokuapp.com/pushMessage?name=${this.firstname}&message=${this.message}&to=${this.to}`
        )
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    filterByTo(role) {
      console.log(role);
      axios
        .get(`https://filechats.herokuapp.com/filterMessageByRole?role=${role}`)
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Montserrat, sans-serif;
  color: #00ffd4;
}

.main-container {
  position: fixed;
}

input[type="text"],
select {
  width: 284px;
  height: 25px;
  padding: 1px 10px;
  box-sizing: border-box;
  border: none;
  border-bottom: 4px solid #00ffd4;
  display: block;
  margin-bottom: 20px;
  background-color: #ffffff00;
  color: white;
}

input[type="SUBMIT"] {
  width: 100%;
  padding: 10px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 14px;
  cursor: pointer;
  border-color: #00ffd4;
  border-style: solid;
  width: 280px;
  background-color: #ffffff00;
}

input[type="submit"]:hover {
  background-color: #00ffd4;
  color: #000000;
}

input[type="submit"] {
  background-color: #ffffff00;
  color: #00ffd4;
  font-weight: bold;
  width: 360px;
}

/* input[type="View"] {
  width: 100%;
  padding: 10px 150px;
  margin: -25px 0;
  border: none;
  border-radius: 14px;
  cursor: pointer;
  border-color: #00ffd4;
  border-style: solid;
  width: 280px;
  background-color: #ffffff00;
} */

/* input[type="View"]:hover {
  background-color: #00ffd4;
  color: #000000;
} */

/* input[type="View"] {
  background-color: #ffffff00;
  color: #00ffd4;
  font-weight: bold;
  width: 360px;
}

input[type="Info"] {
  width: 100%;
  padding: 10px 150px;
  margin: 30px 0;
  border: none;
  border-radius: 14px;
  cursor: pointer;
  border-color: #00ffd4;
  border-style: solid;
  width: 280px;
  background-color: #ffffff00;
}

input[type="Info"]:hover {
  background-color: #00ffd4;
  color: #000000; */
/* }

input[type="Info"] {
  background-color: #ffffff00;
  color: #00ffd4;
  font-weight: bold;
  width: 360px;
} */

form {
  border-radius: 5px;
  height: 265px;
  width: 360px;
  border-color: #00ffd4;
  border-style: solid;
  border-radius: 20px;
  position: fixed;
  top: 30%;
  left: 40%;
  padding-top: 20px;
}

.formword {
  padding-left: 35px;
}
.button {
  padding-top: 25px;
}
.button2 {
  padding: 0px 48px;
  margin: 0px 0px;
  color: #00ffd4;
  text-decoration: underline;
}

.button3 {
  width: 100%;
  padding: 15px 30px;
  color: #00ffd4;
  text-decoration: underline;
}

.button2:hover {
  color: white;
}

.button3:hover {
  color: white;
}

.text {
  font-size: 30px;
}

.title {
  margin-top: -100px;
  margin-bottom: 63px;
  margin-left: 25px;
  font-size: 20px;
}
</style>