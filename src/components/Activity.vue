<template>
  <div class="tableall">
    <el-table
      :data="activities"
      :row-class-name="tableRowColor"
      >

      <el-table-column
          prop="name"
          label="Activities"
          class="actcolumn"
          width="400">
      </el-table-column>

      <el-table-column
          label="Date"
          class="datecolumn">
        <template slot-scope="scope">
          <i class="el-icon-date"></i>
          <span style="margin-left: 10px">{{getDate(scope.row.date)}}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="Remove"
        class="remcolumn">
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
          label="Check"
          class="checkcolumn">
        <template slot-scope="scope">
          <el-button
            type="success"
            icon="el-icon-check"
            @click="completeActivity(scope.row)"
            circle
            size="small">
          </el-button>
        </template>
      </el-table-column>
      <el-table-column
          label="View"
      class="viewcolumn">
        <template slot-scope="scope">
          <el-button
              type="primary"
              icon="el-icon-view"
              circle @click=""
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
        const message = `This action will permanently remove the activity ${item.name}. Continue?`;
        this.$confirm(message, 'Caution', {
          confirmButtonText: 'CONFIRM',
          cancelButtonText: 'Not yet',
          type: 'danger'
        }).then(() => {
          this.deleteActivity({activity: item})
        })
        }
      }

  }
</script>

<style>
.tableall{
  margin-left: 200px;
  margin-right: 200px;
}
.el-table .actcoulm {
  text-align: left;
  padding-right: 100px;
}

.el-table .warning-row {
  background: white;
}

.el-table .success-row {
  background: #f0f9eb;
}



div .cell{
  text-align: center;
}
</style>
