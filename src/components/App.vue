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
          value: 'saved'
        }, {
          title: 'На рассмотрении',
          value: 'processed'
        }, {
          title: 'На доработке',
          value: 'returned'
        }, {
          title: 'Согласована',
          value: 'accepted'
        }, {
          title: 'Не удовлетворена',
          value: 'declined'
        }
      ]
    }
  }
}
</script>

<style>
</style>
