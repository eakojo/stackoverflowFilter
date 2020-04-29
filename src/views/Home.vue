<template>
  <div class="wrapper">
    <div class="navbar">
      <div class="brand">
        <img src="@/assets/brand.png" alt="">
      </div>
      <!-- <div class="search">
        <i class="fas fa-search"></i>
        <input type="text">
      </div> -->
    </div>
    <div class="clearfix"></div>
    <div class="filter-box">
        <div class="input-page">
          <input type="text" v-model="form.page" min="0" max="999" placeholder="Page">
        </div>
        <div class="input-pagesize">
          <input type="text" v-model="form.pagesize" min="0" max="999" placeholder="Pagesize">
        </div>
        <div class="input-fromdate">
          <!-- <i class="far fa-calendar-alt"></i> -->
          <input type="date" v-model="form.fromdate" placeholder="From Date">
        </div>
        <div class="input-todate">
          <!-- <i class="far fa-calendar-alt"></i> -->
          <input type="date" v-model="form.todate" placeholder="To Date">
        </div>
        <div class="input-sort">
          <select name="" id="" v-model="form.sort">
            <option value="votes">Votes</option>
            <option value="activity">Activity</option>
            <option value="creation">Creation</option>
          </select>
        </div>
    </div>
    <div class="filter-box">
      <div class="input-min">
        <!-- <i class="far fa-calendar-alt"></i> -->
        <input type="date" placeholder="Min" v-model="form.min">
      </div>
      <div class="input-max">
        <!-- <i class="far fa-calendar-alt"></i> -->
        <input type="date" placeholder="Max" v-model="form.max">
      </div>
      <div class="input-order">
        <select name="" id="" v-model="form.order">
          <option value="desc">DESC</option>
          <option value="asc">ASC</option>
        </select>
      </div>
      <div class="input-submit" v-if="!submitting" @click="send">Query</div>
      <div class="input-submit" v-else>Quering</div>
    </div>

    <!-- <h2>Advance Search Result</h2> -->
    <div class="result-box">
      <div class="list-item">
        <div class="score"></div>
        <h2 class="title">Function to print the contents of a text file</h2>
      </div>
      <div class="list-item">
        <div class="score"></div>
        <h2 class="title">Function to print the contents of a text file</h2>
      </div>
    </div>
  </div>
</template>

<script>
  import moment from 'moment';

  export default {
    name: 'Home',
    data(){
      return {
        form : {
          page: '',
          pagesize: '',
          fromdate: '',
          todate: '',
          sort: 'votes',
          min: '',
          max: '',
          order: 'desc'
        },
        submitting: false
      }
  },
  methods: {
    send(){
      this.submitting = true
      let payload  = this.form;
      // console.log(payload)
      this.$http.post('https://api-teamwaveassignment.herokuapp.com/api/v1.0/questions_filter', payload)
      .then(res => {
          this.submitting = false
          console.log(res)
      })
      .catch(err => {
          this.error = err.body.message
          this.submitting = false
      })
    },
    toTimestamp(strDate){
      var datum = Date.parse(strDate);
      return datum/1000;
    },

  
  },
  components: {

  }
}
</script>

<style lang="scss">
  .clearfix{
    clear: both;
  }
  .filter-box{
    margin-top: 10px;
    width: 100%;
    height: 45px;
    &>div{
      display: inline-block;
      background-color: #e5e9ec;
      border: none;
      margin-left: 10px;
      input, select{
        width: 100%;
        outline: none;
        border: 1px solid silver;
        padding: 2px;
        border: none;
        padding: 10px;
        background-color: #e5e9ec;
      }
    }
    .input-page{
      width: 40px;
      margin-right: 20px;
    }
    .input-pagesize{
      width: 55px;
      margin-right: 20px;
    }
    .input-fromdate,.input-todate,.input-min, .input-max{
      width: 160px;
      input{
        width: 80%;
      }
    }
    .input-sort{
      width: 90px;
      // height: 40px;
      padding: 0;
      input{
        width: 60%;
      }
    }
  }
  .result-box{
    padding: 10px;
    background-color: rgb(235, 235, 235);
  }
  .list-item{
    background-color: white;
    padding: 20px;
    border-radius: 3px;
    margin-bottom: 10px;
    .title{
      font-size: 1.1em;
      text-align: left;
      margin: 0;
      color: #f58020;
      cursor: pointer;
      &:hover{
        color: silver;
      }
    }
  }
  .input-submit{
    padding: 10px;
    background-color: black !important;
    color: white;
    cursor: pointer;
  }
</style>
