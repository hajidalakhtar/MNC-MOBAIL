
<template>
  <view>
  
    <nb-header :style="{paddingTop:20,height:80}">
      <nb-body>
        <text :style="{color:'white',fontSize:16}">DATA REPORT</text>
      </nb-body>
      <nb-right>
        <nb-button transparent :on-press="()=> about()">
          <nb-icon name="person" />
        </nb-button>
      </nb-right>
    </nb-header>
    <!-- <text class="center" :style="{fontSize:20,marginBottom:30,marginTop:20}">{{username}}</text> -->
    <view :style="{height:515}">
      <nb-Spinner color="green" v-if="loading == true" />
      <scroll-view v-else>
        <nb-Card v-for="datas in data" class="currency" >
          <touchable-opacity :on-press="()=> details(datas)">
            <nb-CardItem>
              <nb-Body>
                <text :style="{fontSize:20,paddingTop:5}">{{ datas.BUILDING_NAME }}</text>
                <text
                  v-if="datas.ADDRESS != null"
                  :style="{fontSize:10,paddingBottom:5,paddingTop:4}"
                >{{ datas. ADDRESS }}</text>

                <text v-else :style="{fontSize:10,paddingBottom:5,paddingTop:4}">Data tidak ada</text>
              </nb-Body>
            </nb-CardItem>
          </touchable-opacity>
        </nb-Card>
      </scroll-view>
    </view>
    <view :style="{flex: 1}">
        <nb-fab 
          :onPress="chart"
          direction="up"
          position="bottomRight"
          :style="{width:60,height:60,borderRadius:100}"
        >
          <nb-icon  name="pie"/>
          <!-- <nb-icon-nb name="md-share"></nb-icon-nb> -->
         
        </nb-fab>

    <!-- <flat-list :data="data" :render-item="(item) => renderList(item)" /> -->
  </view>
</template>

<script>
import React from "react";
import axios from "axios";

import { Text } from "react-native";
export default {
  data() {
    return {
      username: null,
      data: null,
      loading: true,
       isFabIconActive: false,
      stylesObj: {
        fabContainer: {
          position: "bottomRight"
        }
      }
    };
  },
  props: {
    navigation: { type: Object }
  },
  mounted() {
    this.username = this.navigation.state.params.username;

    axios
      .get(
        "http://10.9.23.50:8000/api/report/user?username=" + this.username
        // "http://192.168.0.104:8000/api/report/user?username=" + this.username
      )
      .then(
        response => ((this.data = response.data.data), (this.loading = false))
      );
  },
  methods: {
  
    about: function() {
        this.navigation.navigate("About");
      // this.isFabIconActive = !this.isFabIconActive;
    },
    chart: function() {
        this.navigation.navigate("Chart",{
              username: this.username
            });
      // this.isFabIconActive = !this.isFabIconActive;
    },
    details: function(datas) {
      // console.log(datas.id);

      this.navigation.navigate("Details", {
        ReportId: datas.id
      });
    }
    // renderList: function(item) {
    //   return <Text>{item.BUILDING_NAME}</Text>;
    // }
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
}
</style>