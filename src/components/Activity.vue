<template>
  <div>
    <el-table
      :data="activities"
      :row-class-name="tableRowColor">
      <div class="col">left</div>
      <div class="col text-left">inline content needs to be right aligned</div>
      <el-table-column
        prop="name"
        label="Activities"
        width="300"
        style="text-align: left">
      </el-table-column>
      <el-table-column
          label="Date">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span style="margin-left: 10px">{{getDate(scope.row.date)}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="Remove">
        <template slot-scope="scope">
          <el-button type="danger"
            icon="el-icon-delete"
            @click="openModal(scope.row)"
            circle
            size="small">
          </el-button>
        </template>
      </el-table-column>
      <el-table-column
          label="Check">
        <template slot-scope="scope">
          <el-button
              type="success"
              icon="el-icon-check"
              circle @click=""
              size="small">
          </el-button>
        </template>
      </el-table-column>
      <el-table-column
          label="View">
        <template slot-scope="scope">
          <el-button
              type="primary"
              icon="el-icon-view"
              circle @click="completeActivity(scope.row)"
              size="small">
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
  import {mapGetters, mapActions} from 'vuex'
  import moment from 'moment'
  import uuid from 'uuid/v4'
  export default {
    name: 'Activity',
    data() {
      return {
        activity: '',
        date: '',
      }
    },
    computed: {
      ...mapGetters({
        'activities': 'getActivities'
      }),
    },
    methods: {
      ...mapActions(['addActivity', 'deleteActivity', 'changeActivityState']),
      completeActivity(item) {
        this.changeActivityState({activity: item})
      },

      tableRowColor({row, rowIndex}) {
        if (row.completed === true) {
          return 'success-row';
        } else {
          return 'warning-row'
        }
        return '';
      },

      getDate (item) {
        return moment(item).format('DD/MM/YYYY')
      },

      openModal(item) {
          this.deleteActivity({activity: item})
        }
      }

  }
</script>

<style>
div.cell {
  text-align: center;
}

.el-table .warning-row {
  background: white;
}

.el-table .success-row {
  background: #f0f9eb;
}
</style>
