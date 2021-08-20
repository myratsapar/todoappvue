<template>
  <div>
    <div>
      <el-row type="flex" justify="center" class="counterSection">

      </el-row>
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

.counterSection {
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
}
</style>