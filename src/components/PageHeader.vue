<template>
    <div id="header">
      <div id="header_banner">
        Аеропорт «Львів» 
        <div id="header_banner_bold">+38 (067) 657 47 87 </div>
      </div>
      <div id="header_img">
        <img src="@/assets/logotype.svg" alt="">
      </div>
    </div>
</template>

<script>

export default {
  name: 'PageHeader',
  components: {
    
  }
}
</script>

<style scoped>
#header{
  width: 100vw; height: 100px;
  background-color: #F1F1F1;
  position: fixed;
  top: 35px; left: 0;
  z-index: 999;
}
#header_img{
  height: 100%; width: 35%;
  display: flex; justify-content: center; align-items: center;
}
#header_img > img{
  background-size: 50%;
  height: 60%;
  cursor: pointer;
}

@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200&family=Roboto+Condensed:wght@300&display=swap');
#header_banner{
  position: fixed;
  margin-top: -35px;
  width: 100%; height: 35px;
  display: flex; justify-content: center; align-items: center;
  text-align: center;
  gap: 5px;
  background-color: black;
  color: white;
  font-family: 0.9em;
  font-family: 'Roboto Condensed', sans-serif;
}
#header_banner_bold{
  font-weight: bold;
  cursor: bold;
}

/* Slightly Resized Screen Styles */
@media screen and (max-width: 1200px) {
  #header_img{
    width: 40%;
  }
}

/* Half-Screen Styles */
@media screen and (max-width: 900px) {
  #header_img{
    width: 50%;
  }
}

/* Mobile Styles */
@media screen and (max-width: 768px) {
  #header_img{
    justify-content: flex-end;
    width: 55%;
  }
}
</style>
