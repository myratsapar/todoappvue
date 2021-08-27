<template>
  <div class="main container">
    <h1 class="apptitle">Vue.js todo list project</h1>
    <p class="slogan">I was born to do this</p>

    <div v-if="isWrongActivity" class="wrongNotification">
      <el-alert
        :title="errorMessage"
        type="error"
        :center="true"
        show-icon
        :closable="false">
      </el-alert>
    </div>
    <Input-Section></Input-Section>
    <Activity v-if="!isEmpty"></Activity>
    <Information-Section></Information-Section>

  </div>
</template>

<script>
  import {mapGetters, mapActions} from 'vuex'
  import InputSection from './InputSection'
  import Activity from './Activity'
  import InformationSection from './InformationSection'


  export default {
    name: 'Dashboard',
    components: {
      InputSection,
      Activity,
      InformationSection
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
  font-family: monospace;
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

.slogan{
  margin-top: -10px;
  margin-bottom: 40px;
}
</style>
