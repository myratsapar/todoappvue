<template>
  <div class="main container">
    <h1 class="apptitle">Vue.js todo list</h1>
    <p class="slogan">I was born to do this</p>
    <div v-if="isEmpty">

    </div>

    <div v-if="isWrongActivity" class="wrongNotification">
      <el-alert
        :title="errorMessage"
        type="error"
        :center="true"
        show-icon
        :closable="false">
      </el-alert>
    </div>

    <Activity v-if="!isEmpty"></Activity>
    <Information-Section></Information-Section>
    <Input-Section></Input-Section>
  </div>
</template>

<script>
  import {mapGetters, mapActions} from 'vuex'
  import Activity from './Activity'
  import InformationSection from './InformationSection'
  import InputSection from './InputSection'

  export default {
    name: 'Dashboard',
    components: {
      Activity,
      InformationSection,
      InputSection
    },
    computed: {
      ...mapGetters({
        'activities': 'getActivities',
        'errorMessage': 'getErrorMessage'
      }),
      isEmpty() {
        return this.activities.length === 0;
      },
      isWrongActivity() {
        return this.errorMessage.length > 0;
      }
    },
  }
</script>

<style>
.main {
  text-align: center;
  margin-left: 1rem;
  margin-right: 1rem;
  margin-top: 10px;
}

.wrongNotification {
  margin-bottom: 0.2rem;
  width: 80%;
  margin-left: 10%;
  text-align: center;
  margin-top: 10px;
}
.apptitle{
  text-align: center;
  font-family: monospace;
  margin-top: 150px;
}
.slogan{
  text-align: center;
  font-family: monospace;
  margin-top: -10px;
}
body{
  background: linear-gradient(to right, #00b4db, #0083b0);
}
</style>