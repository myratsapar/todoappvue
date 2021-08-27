<template>
  <div>
    <div>
      <el-row type="flex" justify="start" class="counterSection"> </el-row>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  export default {
    name: 'InformationSection',
    computed: {
      ...mapGetters({
        'activities': 'getActivities'
      }),
      completed() {
        return this.activities.filter((val) => val.completed === true).length;
      },
      total() {
        return this.activities.length;
      },
    },
  }
</script>

<style>


</style>
