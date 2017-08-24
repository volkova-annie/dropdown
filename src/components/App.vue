<template>
  <div id='app'>
    <dropdown-status v-bind:options='options' v-bind:statuses='statuses'></dropdown-status>
  </div>
</template>

<script>
import DropdownStatus from './DropdownStatus.vue'

export default {
  name: 'app',
  components: {
    DropdownStatus
  },
  data() {
    return {
      options: {
        placeholder: 'Статус претензии',
        allTitle: 'Все'
      },
      statuses: [
        {
          title: 'На проверке',
          value: 'saved',
          // isChecked: false
        }, {
          title: 'На рассмотрении',
          value: 'processed',
          // isChecked: false
        }, {
          title: 'На доработке',
          value: 'returned',
          // isChecked: false
        }, {
          title: 'Согласована',
          value: 'accepted',
          // isChecked: false
        }, {
          title: 'Не удовлетворена',
          value: 'declined',
          // isChecked: false
        }
      ]
    }
  }
}
</script>

<style>
</style>
