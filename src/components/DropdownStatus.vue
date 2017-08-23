<template>
  <div class='container'>
    <button type="button" name="button" v-on:click='toggleClass' v-bind:class='[isActive ? "arrow" : "", "dropdown-menu-title"]'>
      <!-- <span class="placeholder">Статус претензии</span> -->
      <span class="placeholder">{{ placeholder }}</span>
    </button>
    <ul id='dropdown-menu' v-bind:class='{"open": isActive}'>
      <li class='dropdown-menu-option' v-for='option in options'>
        <label>
          <input class='dropdown' type='checkbox' v-bind:value='option.value' v-model='option.checked' v-on:click='selectOption(option)'/>{{option.title}}
        </label>
      </li>
    </ul>
  </div>
</template>

<script>


export default {
  data()  {
    return {
      options: [
        {
          title: 'Все',
          id: 1,
          value: '',
          checked: false
        }, {
          title: 'На проверке',
          id: 2,
          value: 'saved',
          checked: false
        }, {
          title: 'На рассмотрении',
          id: 3,
          value: 'processed',
          checked: false
        }, {
          title: 'На доработке',
          id: 4,
          value: 'returned',
          checked: false
        }, {
          title: 'Согласована',
          id: 5,
          value: 'accepted',
          checked: false
        }, {
          title: 'Не удовлетворена',
          id: 6,
          value: 'declined',
          checked: false
        }
      ],
      isActive: false,
      selectedOptions: []
    }
  },
  computed: {
    placeholder() {
      var arr = this.selectedOptions;
      var text = this.selectedOptions.map(el => el.title).join(', ');
      // console.log(text);
      // console.log(arr);
      if (arr.length === 4) {
        // console.log('4 из 5');
      }
      if (arr.length === 6) {
        // console.log('all');
      }
      arr.map(function(el) {
        if (el.id === 1){
          // console.log('hello');
        }
      }
    );
      // if ()
      // return this.selectedOptions.map(el => el.title).join(', ');
    }
  },
  methods: {
    selectOption: function(option) {
      if (option.isChecked) {
        this.selectedOptions = this.selectedOptions.filter(el => el.id !== option.id);
      } else {
        option.isChecked = true;
        this.selectedOptions.push(option);
        console.log(option.checked);
      }
    },
    toggleClass: function() {
      this.isActive = !this.isActive
      console.log(this.options.checked);
    }
  }
}


</script>

<style>
  .container {
    position: absolut;
    width: 200px;
    font-family: Roboto;
    font-size: 16px;
  }
  .dropdown-menu-title {
    position: absolute;
    display: flex;
    justify-content: space-around;
    position: inherit;
    width: 202px;
    color: black;
    margin: 0;
    padding: 0;
    font-family: Roboto;
    font-size: 17px;
    height: 22px;
    font-weight: bold;
    border: 1px solid #000;
    text-align: left;
    background-color: inherit;
    cursor: pointer;
  }
  .dropdown-menu-title:after {
    position: absolute;
    left: 185px;
    top: 12px;
    content: "▼";
    font-size: 14px;
  }
  .dropdown-menu-title:focus {
    outline: none;
  }
  .arrow:after {
    position: absolute;
    left: 185px;
    top: 12px;
    content: "▲";
    font-size: 14px;
  }
  #dropdown-menu {
    display: none;
    width: 200px;
    padding: 0;
    margin: 0;
    list-style: none;
    color: gray;
    border-left: 1px solid #000;
    border-right: 1px solid #000;
  }
  #dropdown-menu.open {
    display: block;
  }
  .open:last-child {
    border-bottom: 1px solid #000;
  }
  ul#dropdown-menu.open:not(:last-child) {
  }
  li.dropdown-menu-option {
    border-bottom: 1px solid #d6d6d6;
    color: gray;
  }
  li.dropdown-menu-option:hover {
    color: black;
  }
  li.dropdown-menu-option:last-child {
    border-bottom: none;
  }
  .placeholder {
    width: 85%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }



</style>
