<template>
  <div id="App" @scroll="handleScroll">
    <div id="scrollDots">
      <div @click="goToPage(1)">
        <div class="scrollDot" id="activedot"></div>
      </div>
      <div @click="goToPage(2)">
        <div class="scrollDot" id=""></div>
      </div>
      <div @click="goToPage(3)">
        <div class="scrollDot" id=""></div>
      </div>
    </div>
    <PageHeader></PageHeader>
    <InventorySearch />

    <div id="fullpage">
      <div id="card_holder">
        <h1 id="card_holder_text">Наш автопарк</h1>
        <VehicleCard v-for="(car, index) in car_list" :key="index" :carType="car.type" :year="car.year" :make="car.make"
          :model="car.model" :series="car.series" :milage="car.milage" :title="car.tite" :vin="car.vin"
          :carImg="car.carImg" :sale="car.onSale" :sold="car.sold" />
      </div>
    </div>
    <div id="fullpage">
      <iframe id="map"
  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d12942.10324544669!2d23.956525055558895!3d49.81251768571921!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x88147ed1b65e55c1!2z0JrQvtC80L_RgNCw0LfQuNC90YvQuSDQm9C10YHQutCw0Y8g0YHQtdC70YzQvdC40Y8sIDEwNCwg0KPQutGA0LDQvNC-0LLRgdC60LDRjyDQvtCx0LvQsNGB0YLRjCwg0J_QvtC70L7QttC00YAg0L7QsdC70LDRgdC60LDRjyDQvtCx0LvQsNGB0YLRjCwg0JzQvtGB0LrQvtCz0L4g0YHQtdC70YzQvdC40Y8sIDQ5MDAw!5e0!3m2!1sen!2sua!4v1669012717247!5m2!1sen!2sua"
  width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy"
  referrerpolicy="no-referrer-when-downgrade"></iframe>


    </div>
  </div>
  <PageFooterMobile :isMobile="isMobileView"/>
</template>

<script>

import PageHeader from '@/components/PageHeader.vue';
import PageFooterMobile from '@/components/PageFooterMobile.vue';
import VehicleCard from '@/components/VehicleCard.vue';
import InventorySearch from '@/components/InventorySearch.vue';

import carlist from '@/assets/carlist.json';
export default {
  name: 'App',
  components: {
    PageHeader,PageFooterMobile,
    VehicleCard,
    InventorySearch,
  },
  data() {
    return {
      car_list: [],
      pageList: [],
      isMobileView: false,
    }
  },
  methods: {
    handleScroll(e) {
      var t = document.getElementsByClassName('scrollDot');
      var h = document.getElementById('App').scrollHeight;
      var section = (e.srcElement.scrollTop / h).toFixed(3);
      section = parseFloat(section);
      if (section > 0.45) {
        //case 3
        this.pageList[0].id = "";
        this.pageList[1].id = "";
        this.pageList[2].id = "activedot";
        for (let i = 0; i < t.length; i++) {
          t[i].style.backgroundColor = "black";
        }
        return;
      }

      if (section < 0.25) {
        //case 1
        this.pageList[0].id = "activedot";
        this.pageList[1].id = "";
        this.pageList[2].id = "";
        for (let i = 0; i < t.length; i++) {
          t[i].style.backgroundColor = "white";
        }
        return;
      }
      else if (section < 0.45 || section > 0.33) {
        //case 2
        this.pageList[0].id = "";
        this.pageList[1].id = "activedot";
        this.pageList[2].id = "";
        for (let i = 0; i < t.length; i++) {
          t[i].style.backgroundColor = "black";
        }
        return;
      }

    },
    goToPage(pageNum) {
      var h = document.getElementById('App');
      switch (pageNum) {
        case 1:
          this.pageList[0].id = "activedot";
          this.pageList[1].id = "";
          this.pageList[2].id = "";
          h.scrollTop = 50;
          break;
        case 2:
          this.pageList[0].id = "";
          this.pageList[1].id = "activedot";
          this.pageList[2].id = "";
          h.scrollTop = 500;
          break;
        case 3:
          this.pageList[0].id = "";
          this.pageList[1].id = "";
          this.pageList[2].id = "activedot";
          h.scrollTop = 2000;
          break;
      }
    },
    checkIfMobile() {
      if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
        return true
      }
      else {
        return false
      }
    },
  },
  mounted() {
    this.car_list = carlist;
    this.pageList = document.getElementsByClassName('scrollDot');
    this.isMobileView = this.checkIfMobile();
    console.log(this.isMobileView);
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  font-family: 'Poppins', sans-serif;
}

body,
html {
  width: 100%;
  height: 100%;
}

#App {
  position: relative;
  scroll-snap-type: y mandatory;
  overflow-y: scroll;
  scroll-behavior: smooth;

  width: 100vw;
  height: 100vh;
}

#card_holder {
  width: 80%; height: 100%;
  display: flex;
  overflow-x: auto;
  justify-content: center;
  align-items: center;
  gap: 30px 30px;
  right: 10px;
  flex-wrap: wrap;
}
#card_holder::-webkit-scrollbar {
  display: flex;
  /* Safari and Chrome */
}

#scrollDots {
  position: fixed;
  right: 0;
  top: 50%;
  transform: translate(-50%, 0);
  display: flex;
  flex-direction: column;
  height: fit-content;
  width: fit-content;
  gap: 10px;
  justify-content: center;
  align-items: center;
  transition: 0.5s ease;
  z-index: 999;
  transition: 0.2s ease;
  padding: 10px;
}

#scrollDots:hover {
  border-radius: 50px;
  background-color: rgba(0, 0, 0, 0.5);
}

#scrollDots:hover>div>div {
  background-color: white !important;
  transition: 0.2s ease;
  background: white;
}

#scrollDots>div {
  width: 20px;
  height: 20px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.scrollDot {
  background-color: white;
  border-radius: 50%;
  width: 5px;
  height: 5px;
  transition: 0.2s ease;
}

.scrollDot:hover {
  width: 10px;
  height: 10px;
}

#activedot {
  width: 15px;
  height: 15px;
}

#fullpage {
  width: 100%;
  height: calc(100vh - 135px);
  scroll-snap-align: start;
  scroll-snap-stop: always;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 135px;

}
#card_holder_text{
  width: 100%;
  text-align: center;
  text-decoration: underline;
}
#map {
  width: 100%;
  height: 100%;
}
::-webkit-scrollbar {
  display: none;
  /* Safari and Chrome */
}



/* Half-Screen Styles */
@media screen and (max-width: 900px) {
  #map {
    width: 100%;
    height: calc(100% - 70px);
    margin-bottom: 70px;
  }
}
</style>
