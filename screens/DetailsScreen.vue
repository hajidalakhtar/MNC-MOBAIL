<template>
  <view>
    <nb-header :style="{paddingTop:20,height:80}">
      <nb-body>
        <text :style="{color:'white',fontSize:16}">DETAILS</text>
      </nb-body>
      <nb-right>
        <nb-button transparent>
          <nb-icon name="pie" />
        </nb-button>
      </nb-right>
    </nb-header>
    <nb-Spinner color="green" v-if="loading == true" />

    <scroll-view v-else>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">BUILDING NAME :</nb-text>
            <nb-text v-if="BuildingName == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{BuildingName}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">PIC MNC :</nb-text>
            <nb-text v-if="PicName == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{PicName}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">PROGRESS STATUS :</nb-text>
            <nb-text v-if="ProgressStatus == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{ProgressStatus}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">COLOR MAP :</nb-text>
            <nb-text v-if="ColorMap == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{ColorMap}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">ADDRESS :</nb-text>
            <nb-text v-if="Address == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Address}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">PROVINCE :</nb-text>
            <nb-text v-if="Province == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Province}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">CITY :</nb-text>
            <nb-text v-if="City == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{City}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">SUBDISTRICT :</nb-text>
            <nb-text v-if="Subdistrict == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Subdistrict}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">COORDINATE :</nb-text>
            <nb-text v-if="Coordinate == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Coordinate}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">PROPERTY TYPE :</nb-text>
            <nb-text v-if="PropertyType == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{PropertyType}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">DEVELOPER :</nb-text>
            <nb-text v-if="Developer == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Developer}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">NAME :</nb-text>
            <nb-text v-if="Name == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Name}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
      <nb-card>
        <nb-card-item>
          <nb-body>
            <nb-text :style="{fontSize:12}">EMAIL :</nb-text>
            <nb-text v-if="Email == null">Data tidak ada</nb-text>
            <nb-text v-else :style="{fontSize:19}">{{Email}}</nb-text>
          </nb-body>
        </nb-card-item>
      </nb-card>
    </scroll-view>
  </view>
</template>
<script>
import React from "react";
import axios from "axios";

import { Text } from "react-native";
export default {
  data() {
    return {
      loading: true,
      ReportId: null,
      data: null,
      BuildingName: null,
      PicName: null,
      ProgressStatus: null,
      ColorMap: null,
      Address: null,
      Province: null,
      City: null,
      Subdistrict: null,
      Coordinate: null,
      PropertyType: null,
      Developer: null,
      Name: null,
      Email: null
    };
  },
  props: {
    navigation: { type: Object }
  },
  mounted() {
    this.ReportId = this.navigation.state.params.ReportId;
    console.log("http://10.9.23.50:8000/apireport/" + this.ReportId)
    axios
     
      // .get("http://192.168.0.104:8000/apireport/" + this.ReportId)
      .get("http://10.9.23.50:8000/apireport/" + this.ReportId)
      .then(
        response => (
          (console.log(response.data)),
          (this.data = response.data),
          ((this.BuildingName = this.data.BUILDING_NAME),
          (this.PicName = this.data.PIC_MNC),
          (this.ProgressStatus = this.data.PROGRESS_STATUS),
          (this.ColorMap = this.data.COLOR_MAP),
          (this.Address = this.data.ADDRESS),
          (this.Province = this.data.PROVINCE),
          (this.City = this.data.CITY),
          (this.Subdistrict = this.data.SUBDISTRICT),
          (this.Coordinate = this.data.COORDINATE),
          (this.PropertyType = this.data.PROPERTY_TYPE),
          (this.Developer = this.data.DEVELOPER),
          (this.Name = this.data.NAME),
          ((this.Email = this.email), (this.loading = false)))
        )
      );
  },
  methods: {}
};
</script>
<style>
.container {
  align-items: center;
  justify-content: center;
  flex: 1;
}
.heading {
  font-size: 30px;
  font-weight: bold;
  color: darkolivegreen;
  margin: 20px;
}
</style>