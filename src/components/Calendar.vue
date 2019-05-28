<template>
  <div class="c-wrap">
    <div class="c-header">
      <div class="arrow" @click="preMonth"> &LeftAngleBracket;
      </div>
      <div class="detail">
        <div class="year">{{active.year}}</div>
        <div class="date">{{active.month}} 月</div>
      </div>
      <div class="arrow" @click="nextMonth">
        &RightAngleBracket;
      </div>
    </div>
    <div class="c-body">
      <div class="c-body-week">
        <div class="c-body-week-label" v-for=" w in weekList">{{w}}</div>
      </div>
      <div class="c-body-day">
        <div class="c-body-row" v-for="week in weeks">
          <div class="c-body-date"
               :class="{ placeholder: d.month != active.month, today: d.year == new Date().getFullYear() && d.date == new Date().getDate() && d.month == new Date().getMonth()+1, active: d.date == active.date && d.month == active.month }"
               v-for="d in week"
               @click="dateClicked"
               :data-year="d.year"
               :data-month="d.month"
               :data-date="d.date"
          >{{d.date}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      _activeDate: {
        type: Object,
        default: null,
        validator: function (value) {
          return value.hasOwnProperty('year') && value.hasOwnProperty('month') && value.hasOwnProperty('date')
        }
      },
      debug: {
        type: Boolean,
        default: false
      }
    },
    data: function () {
      return {
        today: new Date(),
        active: {
          year: new Date().getFullYear(),
          month: new Date().getMonth()+1,
          date: new Date().getDate()
        },
        weekList: [
            '日','一','二','三','四','五','六'
        ]
      }
    },
    methods: {
      dateClicked: function (e) {
          let targetYear = e.target.dataset.year;
          let targetMonth = e.target.dataset.month;
          let targetDate = e.target.dataset.date;
//        console.log(e.target.dataset)
          this.active.year = targetYear;
          this.active.month = targetMonth;
          this.active.date = targetDate;

          let to = {
              year: targetYear,
              month: targetMonth,
              date: targetDate
          };
          this.debug && console.info('Event: dateChanged', to);
        this.$emit('dateChanged',to )
      },
      preMonth: function () {
        // 上一月

//        当前 年月 可读值
          var _year = this.active.year;
          var _month = this.active.month;

//
          var p_Date = new Date(_year, _month - 2);

        var from = {
            year: this.active.year,
            month: this.active.month
        }
        var to = {
            year: p_Date.getFullYear(),
            month: p_Date.getMonth()+1
        }
        this.active = {
            year: to.year,
            month: to.month,
            date: this.active.date
        }
        if(this.debug){
          console.group('Evnt:month change')
          console.log('from', from)
          console.log('to', to)
          console.groupEnd()
        }
        this.$emit('SwitchPreviousMonth',from , to)
      },
      nextMonth: function () {
        var _year = this.active.year
        var _month = this.active.month

//        下月日期对象
        var n_Date = new Date(_year, _month)

        var from = {
          year: this.active.year,
          month: this.active.month
        }
        var to = {
          year: n_Date.getFullYear(),
          month: n_Date.getMonth()+1
        }
        this.active = {
          year: to.year,
          month: to.month,
          date: this.active.date
        }
        if(this.debug){
          console.group('Evnt:month change')
          console.log('from', from)
          console.log('to', to)
          console.groupEnd()
        }
        this.$emit('SwitchNextMonth',from , to)
      }
    },
    computed: {
      activeDate: function () {
        if(this._activeDate == null || this._activeDate === 'undefined'){
            return {
              year: this.today.year,
              month: this.today.month,
              date: this.today.date,
              day: this.today.day
            }
        }
        return this._activeDate
      },
      weeks: function () {
        var days = {}
//        当前月份第一天星期
        var firstDay = new Date(this.active.year, this.active.month-1, 1).getDay()
//        console.log('first day',firstDay)
        var preMonthDays = []
        for(var i = firstDay-1; i >= 0; i--){
            preMonthDays.push({
                'year': this.active.year,
                'month': this.active.month-1,
                'date': new Date(this.active.year, this.active.month-1, -i).getDate()
            })
        }

        var currentMonthDays = []
        for(var i=1; i<= new Date(this.active.year, this.active.month, 0).getDate();i++){
          currentMonthDays.push({
            year: this.active.year,
            month: this.active.month,
            date: i
          })
        }
//        console.log(currentMonthDays)
          let nextMonthDays = [];
          let endDay = new Date(this.active.year, this.active.month, 0).getDay();
        for(let i=1; i<7-endDay; i++){
//            console.log(i)
            nextMonthDays.push({
              year: this.active.year,
              month: parseInt(this.active.month)+1,
              date: i
            })
        }

        let totalDate = [];
        totalDate = totalDate.concat(preMonthDays, currentMonthDays, nextMonthDays);

          let weeks = [];
        for(let i = 0; i<totalDate.length; i++){
            if(i%7 === 0){
                weeks[parseInt(i/7)] = new Array(7)
            }
            weeks[parseInt(i/7)][i%7] = totalDate[i]
        }
        return weeks;
      }
    }
  }
</script>

<style scoped>
  *{
    cursor: default;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
  .c-wrap{
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    width: 330px;
    box-shadow: 0px 0px 2px grey;
    text-align: center;
  }
  .c-header{
    height:100px;
    width: 100%;
    background: #00B8EC;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
  .c-header .arrow{
    font-size: 2.5rem;
    color: #fff;
    padding: 1.55rem;
  }
  .c-header .arrow:hover{
    /*text-decoration: underline;*/
  }
  .c-header .detail{
    color: #fff;
    font-size: 2.56rem;
  }
  .c-header .detail .year{
    font-size: 2.5rem;
  }
  .c-body{
    flex:1;
    width: 100%;
    background-color: #fff;
  }
  .c-body-week{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
    background-color: #00B8EC;
  }
  .c-body-week-label{
    padding: 1rem;
    color: #fff;
  }
  .c-body-week-label:hover{
  }
  .c-body-row{
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
  }
  .c-body-date{
    line-height: 40px;
    font-size: 1.5rem;
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
  .c-body-date:active{
    background-color: aliceblue;
  }
  .c-body-date.placeholder{
    color: #aeaeae;
  }
  .c-body-date.today{
    font-weight: bold;
    color: deepskyblue;
  }
  .c-body-date.active{
    background-color: #00B8EC;
    color: #fff;
  }
  .c-body-date:hover{
    background-color: #46ecb9;
    color: #fff;
    -webkit-transition: background-color 0.3s;
    -moz-transition: background-color 0.3s;
    -ms-transition: background-color 0.3s;
    -o-transition: background-color 0.3s;
    transition: background-color 0.3s;
  }

</style>
