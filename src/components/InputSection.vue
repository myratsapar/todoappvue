<template>
  <div>
    <el-row>
      <el-col :span="8">
        <el-input
          placeholder="What needs to be done"
          v-model="activity"
          size="mini">
        </el-input>
      </el-col>

    </el-row>
    <el-button
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

      setMessageError() {
        let error = '';
        if (this.activity === '') {
          error = 'The activity && the date are empty';

        } else {
          if (this.activity === '') {
            error = 'The activity is empty';
          }
        }

        this.setErrorMessageAction({message: error});
      },
    }
  }
</script>

<style>
</style>