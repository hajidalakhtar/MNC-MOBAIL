
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
        <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">PIC MNC</text>
              <text class="center">{{username}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
      <view :style="{flex: 1, flexDirection: 'row'}" class="container">
      <view  :style="{width:178}">
        <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL SITE SURVEY</text>
              <text class="center">{{data.site_survey}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
            <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL BOQ</text>
              <text class="center">{{data.boq}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
            <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL PNL</text>
              <text class="center">{{data.pnl}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
            <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL NEGOTIATION</text>
              <text class="center">{{data.negotiation}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
      </view>
 <view  :style="{width:178}">
        <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL PKS REVIEW</text>
              <text class="center">{{data.pks_review}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
            <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL SIGN PKS</text>
              <text class="center">{{data.Sign_pks}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
            <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL SELL</text>
              <text class="center">{{data.sell}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
            <nb-Card >
            <nb-CardItem>
              <nb-Body>
              <text class="center">TOTAL REJECT</text>
              <text class="center">{{data.reject}}</text>
              </nb-Body>
            </nb-CardItem>
        </nb-Card>
      </view>

   
      </view>

      </scroll-view>
    </view>
    <view :style="{flex: 1}">
        <nb-fab 
          :onPress="chart"
          direction="up"
          position="bottomRight"
          :style="{width:60,height:60,borderRadius:100}"
        >
          <nb-icon  name="home"/>
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
       
        "http://10.9.23.50:8000/api/user?username=" + this.username
        // "http://192.168.0.104:8000/api/report/user?username=" + this.username
        // "http://192.168.0.104:8000/api/user?username=" + this.username
      )
      .then(
        response => ((this.data = response.data), (this.loading = false))
      );
  },
  methods: {
  
    about: function() {
        this.navigation.navigate("About");
      // this.isFabIconActive = !this.isFabIconActive;
    },
    chart: function() {
        this.navigation.navigate("Report",{
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