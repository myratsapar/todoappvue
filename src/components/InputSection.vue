<template>
  <div>
      <el-col :span="7">
        <el-input
          class="addbar"
          placeholder="What needs to be done"
          v-model="activity"
          size="mini">
        </el-input>
      </el-col>

    <el-date-picker
          id="duedate"
          v-model="date"
          type="date"
          size="mini"
          placeholder="Due Date">
      </el-date-picker>

    <el-button
        id="plusbutton"
        type="primary"
        icon="el-icon-circle-plus-outline"
        circle
        @click="addActivityMethod()">
    </el-button>

  </div>
</template>

<script>
  import { mapActions } from 'vuex'
  import uuid from 'uuid/v4'

  export default {
    name: 'InputSection',
    data() {
      return {
        activity: '',
        date: '',
      }
    },
    methods: {
      ...mapActions(['addActivity', 'setErrorMessageAction']),
      addActivityMethod() {
        if (this.validateData() === true) {
          const activity = {
            name: this.activity,
            completed: false,
            date: this.date,
            id: uuid()
          };
          this.setErrorMessageAction({message: ''});

          this.addActivity({activity});
          this.activity = '';


        } else {
          this.setMessageError();
        }
      },

      validateData() {
        if (this.activity !== '') {
          return true;
        } else {
          return false;
        }
      },
    }
  }
</script>

<style>
.addbar {
  margin-top: 9px;
  margin-left: 240px;
  margin-bottom: 30px;
}

#plusbutton{
  margin-left: 50px;
}

#duedate{
  font-family: monospace;

}
</style>
