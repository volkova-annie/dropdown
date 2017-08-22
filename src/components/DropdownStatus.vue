<template>
  <div>
    <ul id='dropdown-menu'>
      <span>Претензии</span>
      <li class='dropdown-menu-option' v-on:click='addOption' v-for='option in options' v-bind:value='[option.id]'><input  class='dropdown' type="checkbox" name=""/>{{option.title}}</li>
    </ul>
  </div>
</template>

<script>
const claim = []

export default {
  data()  {
    return {
      options: [
        {
          title: 'Все',
          id: 1
        }, {
          title: 'На проверке',
          id: 2
        }, {
          title: 'На рассмотрении',
          id: 3
        }, {
          title: 'На доработке',
          id: 4
        }, {
          title: 'Согласована',
          id: 5
        }, {
          title: 'Не удовлетворена',
          id: 6
        }
      ]
    }
  },
  methods: {
    addOption: function() {
      console.log(this.value);
      claim.push({
        title: this.options
      })
      // console.log(claim);
    }
  }

//

//   data() {
//     return {
//       data
//     }
//   },
//   methods: {
//
//     }
}

</script>

<style>

  ul#dropdown-menu {
    display: block;
    border: 1px solid black;
    width: 150px;
    padding: 1px 5px;
    list-style: none;
    color: gray;
  }
  li.dropdown-menu-option {
    display: none;
    border-bottom: 1px solid gray;
    width: calc(100% + 10px);
    margin-left: -5px;
  }
  li.dropdown-menu-option:first-child {
    border-top: 1px solid gray;
  }
  li.dropdown-menu-option:last-child {
    border-bottom: none;
  }
  ul#dropdown-menu:hover > .dropdown-menu-option {
    display: block;
  }
  li.dropdown-menu-option:hover {
    color: black;
  }


</style>
