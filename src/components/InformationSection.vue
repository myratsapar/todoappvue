<template>
  <div>
    <div class="elrow">
      <el-row type="flex" justify="start" class="counterSection" width = "50px"> </el-row>
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
.elrow {
  width: 10%;
}

</style>
