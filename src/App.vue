<template>
  <MainHeader />
  <div id="app" class="container">
    <div class="content">
      <ProfileFoto />
      <MySelf />
    </div>
    <div class="modules-container">
      <Topfact6Module />
      <MyTasks />
    </div>
    <div class="modules-container">
      <Ausbildungsstand />
      <FuturePlans />
    </div>
    <div class="modules-container">
      <Technologie />
      <ProjektTracking />
    </div>
    <div class="modules-container">
      <TopfactStandardsAPI/>
    </div>
  </div>
  <SocialMedia />
</template>

<script>
import Ausbildungsstand from "./components/Ausbildungsstand.vue";
import FuturePlans from "./components/FuturePlans.vue";
import MainHeader from "./components/MainHeader.vue";
import MySelf from "./components/MySelf.vue";
import MyTasks from "./components/MyTasks.vue";
import ProfileFoto from "./components/ProfileFoto.vue";
import Topfact6Module from "./components/topfact6Module.vue";
import Technologie from "./components/Technologie.vue";
import ProjektTracking from "./components/ProjektTracking.vue";
import SocialMedia from "./components/SocialMedia.vue";
import TopfactStandardsAPI from "./components/topfactStandardsAPI.vue";

export default {
  name: "App",
  components: {
    MainHeader,
    ProfileFoto,
    MySelf,
    Topfact6Module,
    MyTasks,
    Ausbildungsstand,
    FuturePlans,
    Technologie,
    ProjektTracking,
    SocialMedia,
    TopfactStandardsAPI
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("https://fluentsupport.com/wp-content/uploads/2024/01/Code-Review-Tools.webp");
  background-size: cover;
  background-position: center;
  min-height: 100vh;
  color: #2c3e50;
}

.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  padding: 20px;
}

header {
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}

.content {
  display: flex;
  flex-direction: row;
  flex: 1;
  padding: 20px;
  gap: 20px;
}

.ProfileFoto {
  width: 200px;
  height: 200px;
  background-color: #ccc;
  border-radius: 50%;
}

.MySelf {
  flex: 1;
  background-color: #f4f4f4;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.modules-container {
  display: flex;
  gap: 20px;
  margin-top: 30px;
}

.modules-container > * {
  flex: 1;
  background-color: #f4f4f4;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

@media (max-width: 768px) {
  .content {
    flex-direction: column;
    align-items: center;
  }

  .ProfileFoto {
    width: 150px;
    height: 150px;
    margin-bottom: 20px;
  }

  .MySelf {
    width: 100%;
  }

  .modules-container {
    flex-direction: column;
    align-items: center;
    gap: 20px;
  }
}
</style>
