<template>
  <q-card>
    <q-card-section>
      <div class="text-h5"> Scheduler </div>
      <div class="text-subtitle1"> Configure when the event will be scheduled. </div>
    </q-card-section>
    <q-separator />
    <!-- Option Repeat Types -->
    <q-card-section>
      <!-- Validity  -->
      <div class="q-mb-md">
        <p>
          Validity:
        </p>
        <div class="row">
          <div class="col-2 text-bold q-pt-lg"> From: </div>
          <div class="col">
            <q-input type="number" v-model="start" clearable hint="Optional. Enter the number of days from the start." @input="update()" />
          </div>
        </div>
        <div class="row">
          <div class="col-2 text-bold q-pt-lg"> To: </div>
          <div class="col">
            <q-input type="number" v-model="until" clearable hint="Optional. In number of days from the start. If To and Occurrences are not specified, this task will run until the end date of the study." @input="update()" />
          </div>
        </div>
        <div class="row">
          <div class="col-2 text-bold q-pt-lg"> Occurrences: </div>
          <div class="col">
            <q-input type="number" v-model="occurrences" clearable hint="Optional. The maximum number of occurrences. If Occurrences and To are not specified, this task will run until the end date of the study." @input="update()" />
          </div>
        </div>
      </div>
      <q-separator />
      <p class="q-mt-lg">
        Recurrence:
      </p>
      <div class="row">
        <div class="col-2 text-bold q-pt-lg"> Frequency: </div>
        <div class="col">
          <q-select type="number" v-model="intervalType" :options="intervalTypeOptions" emit-value map-options hint="Enter the desired frequency." @input="update()" />
        </div>
      </div>
      <div class="row">
        <div class="col-2 text-bold q-pt-lg"> Interval: </div>
        <div class="col">
          <q-select @input="update()" v-show="intervalType == 'd'" emit-value map-options  v-model="dailyInterval" :options="dailyIntervalOptions" />
          <q-select @input="update()" v-show="intervalType == 'w'" emit-value map-options  v-model="weeklyInterval" :options="weeklyIntervalOptions" />
          <q-select @input="update()" v-show="intervalType == 'm'" emit-value map-options  v-model="monthlyInterval" :options="monthlyIntervalOptions" />
          <q-select @input="update()" v-show="intervalType == 'y'" emit-value map-options  v-model="yearlyInterval" :options="yearlyIntervalOptions" />
        </div>
      </div>
      <div class="row">
        <div class="col-2 text-bold q-pt-lg"> Week days: </div>
        <div class="col">
          <q-field hint="Optional. Specify the days in the week when this task is allowed. If not specified, all week days are eligible.">
            <div class="row">
              <q-checkbox v-for="(opt, ind) in weekDaysOpts" :key="ind" @input="update()" v-model="weekDays" :val="opt.value" :label="opt.label" />
            </div>
          </q-field>
        </div>
      </div>
      <div class="row">
        <div class="col-2 text-bold q-pt-lg"> Months: </div>
        <div class="col">
          <q-field hint="Optional. Specify months.">
            <div class="row">
              <q-checkbox v-for="(monOpt, ind2) in monthsOpts" :key="ind2" @input="update()" v-model="months" :val="monOpt.value" :label="monOpt.label" />
            </div>
          </q-field>
        </div>
      </div>
      <div class="row">
        <div class="col-2 text-bold q-pt-lg"> Days of the month:: </div>
        <div class="col">
          <q-field hint="Optional. Specify the days of the month when this task is allowed.">
            <div class="row">
              <q-checkbox v-for="monthday in 31" :key="monthday" @input="update()" v-model="monthDays" :val="monthday" :label="monthday.toString()" />
            </div>
          </q-field>
        </div>
      </div>
  </q-card-section>
</q-card>
</template>

<script>
export default {
  name: 'Scheduler',
  props: ['value'],
  data () {
    return {
      startDelaySecs: this.value.startDelaySecs,
      validitySecs: this.value.untilSecs,
      occurrences: this.value.occurrences,
      intervalType: this.value.intervalType,
      intervalTypeOptions: [
        {
          label: 'Daily',
          value: 'd'
        },
        {
          label: 'Weekly',
          value: 'w'
        },
        {
          label: 'Monthly',
          value: 'm'
        },
        {
          label: 'Yearly',
          value: 'y'
        }
      ],

      dailyInterval: this.value.interval ? this.value.interval.toString() : undefined,
      dailyIntervalOptions: [
        {
          label: 'Every day',
          value: '1'
        },
        {
          label: 'Every other day',
          value: '2'
        },
        {
          label: 'Every 3rd day',
          value: '3'
        },
        {
          label: 'Every 4th day',
          value: '4'
        },
        {
          label: 'Every 5th day',
          value: '5'
        },
        {
          label: 'Every 6th day',
          value: '6'
        },
        {
          label: 'Every 7th day',
          value: '7'
        },
        {
          label: 'Every 8th day',
          value: '8'
        },
        {
          label: 'Every 9th day',
          value: '9'
        },
        {
          label: 'Every 10th day',
          value: '10'
        },
        {
          label: 'Every 11th day',
          value: '11'
        },
        {
          label: 'Every 12th day',
          value: '12'
        },
        {
          label: 'Every 13th day',
          value: '13'
        },
        {
          label: 'Every 14th day',
          value: '14'
        },
        {
          label: 'Every 15th day',
          value: '15'
        },
        {
          label: 'Every 16th day',
          value: '16'
        },
        {
          label: 'Every 17th day',
          value: '17'
        },
        {
          label: 'Every 18th day',
          value: '18'
        },
        {
          label: 'Every 19th day',
          value: '19'
        },
        {
          label: 'Every 20th day',
          value: '20'
        },
        {
          label: 'Every 21th day',
          value: '21'
        },
        {
          label: 'Every 22th day',
          value: '22'
        },
        {
          label: 'Every 23th day',
          value: '23'
        },
        {
          label: 'Every 24th day',
          value: '24'
        },
        {
          label: 'Every 25th day',
          value: '25'
        },
        {
          label: 'Every 26th day',
          value: '26'
        },
        {
          label: 'Every 27th day',
          value: '27'
        },
        {
          label: 'Every 28th day',
          value: '28'
        },
        {
          label: 'Every 29th day',
          value: '29'
        },
        {
          label: 'Every 30th day',
          value: '30'
        }
      ],

      weeklyInterval: this.value.interval ? this.value.interval.toString() : undefined,
      weeklyIntervalOptions: [
        {
          label: 'Every week',
          value: '1'
        },
        {
          label: 'Every other week',
          value: '2'
        },
        {
          label: 'Every 3rd week',
          value: '3'
        },
        {
          label: 'Every 4th week',
          value: '4'
        },
        {
          label: 'Every 5th week',
          value: '5'
        },
        {
          label: 'Every 6th week',
          value: '6'
        },
        {
          label: 'Every 7th week',
          value: '7'
        },
        {
          label: 'Every 8th week',
          value: '8'
        },
        {
          label: 'Every 9th week',
          value: '9'
        },
        {
          label: 'Every 10th week',
          value: '10'
        },
        {
          label: 'Every 11th week',
          value: '11'
        },
        {
          label: 'Every 12th week',
          value: '12'
        },
        {
          label: 'Every 13th week',
          value: '13'
        },
        {
          label: 'Every 14th week',
          value: '14'
        },
        {
          label: 'Every 15th week',
          value: '15'
        },
        {
          label: 'Every 16th week',
          value: '16'
        },
        {
          label: 'Every 17th week',
          value: '17'
        },
        {
          label: 'Every 18th week',
          value: '18'
        },
        {
          label: 'Every 19th week',
          value: '19'
        },
        {
          label: 'Every 20th week',
          value: '20'
        },
        {
          label: 'Every 21th week',
          value: '21'
        },
        {
          label: 'Every 22th week',
          value: '22'
        },
        {
          label: 'Every 23th week',
          value: '23'
        },
        {
          label: 'Every 24th week',
          value: '24'
        },
        {
          label: 'Every 25th week',
          value: '25'
        },
        {
          label: 'Every 26th week',
          value: '26'
        }
      ],

      monthlyInterval: this.value.interval ? this.value.interval.toString() : undefined,
      monthlyIntervalOptions: [
        {
          label: 'Every month',
          value: '1'
        },
        {
          label: 'Every other month',
          value: '2'
        },
        {
          label: 'Every 3rd month',
          value: '3'
        },
        {
          label: 'Every 4th month',
          value: '4'
        },
        {
          label: 'Every 5th month',
          value: '5'
        },
        {
          label: 'Every 6th month',
          value: '6'
        },
        {
          label: 'Every 7th month',
          value: '7'
        },
        {
          label: 'Every 8th month',
          value: '8'
        },
        {
          label: 'Every 9th month',
          value: '9'
        },
        {
          label: 'Every 10th month',
          value: '10'
        },
        {
          label: 'Every 11th month',
          value: '11'
        },
        {
          label: 'Every 12th month',
          value: '12'
        },
        {
          label: 'Every 18th month',
          value: '18'
        },
        {
          label: 'Every 24th month',
          value: '24'
        },
        {
          label: 'Every 36th month',
          value: '36'
        },
        {
          label: 'Every 48th month',
          value: '48'
        }
      ],

      yearlyInterval: this.value.interval ? this.value.interval.toString() : undefined,
      yearlyIntervalOptions: [
        {
          label: 'Every year',
          value: '1'
        },
        {
          label: 'Every other year',
          value: '2'
        },
        {
          label: 'Every 3rd year',
          value: '3'
        },
        {
          label: 'Every 4th year',
          value: '4'
        },
        {
          label: 'Every 5th year',
          value: '5'
        },
        {
          label: 'Every 6th year',
          value: '6'
        },
        {
          label: 'Every 7th year',
          value: '7'
        },
        {
          label: 'Every 8th year',
          value: '8'
        },
        {
          label: 'Every 9th year',
          value: '9'
        },
        {
          label: 'Every 10th year',
          value: '10'
        }
      ],

      weekDays: this.value.weekDays,
      weekDaysOpts: [
        {
          label: 'Monday',
          value: 'mo'
        },
        {
          label: 'Tuesday',
          value: 'tu'
        },
        {
          label: 'Wednesday',
          value: 'we'
        },
        {
          label: 'Thursday',
          value: 'th'
        },
        {
          label: 'Friday',
          value: 'fr'
        },
        {
          label: 'Saturday',
          value: 'sa'
        },
        {
          label: 'Sunday',
          value: 'su'
        }
      ],

      months: this.value.months,
      monthsOpts: [
        {
          label: 'January',
          value: '1'
        },
        {
          label: 'February',
          value: '2'
        },
        {
          label: 'March',
          value: '3'
        },
        {
          label: 'April',
          value: '4'
        },
        {
          label: 'May',
          value: '5'
        },
        {
          label: 'June',
          value: '6'
        },
        {
          label: 'July',
          value: '7'
        },
        {
          label: 'August',
          value: '8'
        },
        {
          label: 'September',
          value: '9'
        },
        {
          label: 'October',
          value: '10'
        },
        {
          label: 'November',
          value: '11'
        },
        {
          label: 'December',
          value: '12'
        }
      ],

      monthDays: this.value.monthDays
    }
  },
  computed: {
    start: {
      get () {
        return Math.floor(this.startDelaySecs / (24 * 60 * 60))
      },
      set (days) {
        this.startDelaySecs = days * (24 * 60 * 60)
      }
    },
    until: {
      get () {
        return Math.floor(this.validitySecs / (24 * 60 * 60))
      },
      set (days) {
        this.validitySecs = days * (24 * 60 * 60)
      }
    }
  },
  methods: {
    update () {
      let v = {
        startEvent: 'consent',
        startDelaySecs: isNaN(this.startDelaySecs) ? undefined : this.startDelaySecs,
        untilSecs: isNaN(this.validitySecs) ? undefined : this.validitySecs,
        occurrences: isNaN(this.occurrences) ? undefined : this.occurrences,
        intervalType: this.intervalType,
        months: this.months,
        monthDays: this.monthDays,
        weekDays: this.weekDays
      }
      if (v.intervalType === 'd') v.interval = isNaN(this.dailyInterval) ? undefined : parseInt(this.dailyInterval)
      if (v.intervalType === 'w') v.interval = isNaN(this.weeklyInterval) ? undefined : parseInt(this.weeklyInterval)
      if (v.intervalType === 'm') v.interval = isNaN(this.monthlyInterval) ? undefined : parseInt(this.monthlyInterval)
      if (v.intervalType === 'y') v.interval = isNaN(this.yearlyInterval) ? undefined : parseInt(this.yearlyInterval)
      this.$emit('input', v)
    }
  }
}
</script>
