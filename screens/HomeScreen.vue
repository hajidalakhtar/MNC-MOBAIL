
<template>
  <view :style="{backgroundColor: '#d4e2fa',height:1000}">
    <image
      class="center"
      :style="{width: 120, height: 120,marginTop:50 }"
      :source="{uri: 'http://mncplaysurabaya99.id.tc/wp-content/uploads/sites/447/2016/03/MNC_Playmedia-home.png'}"
    />
    <nb-Card :style="{marginTop:30,height:300,zIndex: 1 }" class="contanier">
      <text class="center" :style="{fontSize:25,}">Login</text>
      <nb-spinner v-if="loading" color="green" />
      <nb-CardItem v-else>
        <nb-Content :style="{marginTop:10}">
          <nb-Item regular>
            <nb-Input :style="{paddingLeft:20}" placeholder="Username" v-model="username" />
          </nb-Item>
          <nb-Item regular :style="{marginTop:10,marginBottom:20}">
            <nb-Input
              :style="{paddingLeft:20}"
              secureTextEntry
              placeholder="Password"
              v-model="password"
            />
          </nb-Item>
          <button success rounded :style="{marginTop:30}" title="Login" :onPress="Login">
            <!-- <Text :style="{color:color.white,marginLeft:120,fontSize:18}">Login</Text> -->
          </button>
        </nb-Content>
      </nb-CardItem>
    </nb-Card>
  </view>
</template>
<script>
import React from "react";
import { Toast } from "native-base";
import axios from "axios";
import { Alert } from "react-native";
export default {
  props: {
    navigation: { type: Object }
  },
  data() {
    return {
      color: {
        white: "white",
        bluegrey: "#263238"
      },
      username: null,
      password: null,
      loading: false
      // data: null
    };
  },

  // mounted() {

  // },
  methods: {
    goToAndroidTabNavigator() {
      this.navigation.navigate("AndroidTabs");
    },
    Login() {
      this.loading = true;
      console.log(this.password)
      axios

        .post("http://10.9.23.50:8000/api/login", {
        // .post("http://192.168.0.104:8000/api/login", {
          username: this.username,
          password: this.password
        })
        .then(response => {
          // JSON responses are automatically parsed.
          // this.data = ;
          console.log(response.data.status);

          if (response.data.status == 200) {
            this.loading = false;
            this.navigation.navigate("Report", {
              username: this.username
            });
          } else {
           Alert.alert(
                'Password Salah !!',
                'Silahkan Tanya Admin',
                [
                    {text: 'OK', onPress: () =>  this.loading = false},
                ],
                { cancelable: false }
            );
          }
          
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  }
};
</script>

<style>
.container {
  align-items: center;
  justify-content: center;
  flex: 1;
}

.center {
  margin-top: 10px;
  /* display: block; */
  margin-left: auto;
  margin-right: auto;
  /* width: 50%; */
}
.contanier {
  /* display: block; */
  margin-left: auto;
  margin-right: auto;
  width: 90%;
  /* height: 200px; */
}
</style>