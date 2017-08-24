<template>
  <div class='container'>
    <button type="button" name="button" v-on:click='toggleClass' v-bind:class='[isActive ? "arrow" : "", "dropdown-menu-title"]'>
      <span class="placeholder">{{ options.placeholder }}</span>
    </button>
    <ul id='dropdown-menu' v-bind:class='{"open": isActive}'>
      <li class='dropdown-menu-option' >
        <label>
          <input class='dropdown' type='checkbox' v-model='isAllChecked' v-on:click='selectAll()'/>{{options.allTitle}}
        </label>
      </li>
      <li class='dropdown-menu-option' v-for='option in statuses' >
        <label>
          <input class='dropdown' type='checkbox' v-bind:value='option.value' v-model='option.isChecked' @click='onSelect(option)'/>{{option.title}} {{option.isChecked?'true':'false'}}
        </label>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  props: ['options', 'statuses'],
  data: function () {
    return {
      isAllChecked: false,
      isActive: false,
      checkedStatuses: []
    }
  },
  computed: {
    // localStatuses() {
    //   const temp = this.statuses.map(el => {
    //     el.isChecked = !!el.isChecked;
    //     return el;
    //   })
    //   console.log(temp);
    //   return temp;
    // },
    placeholder() {
      const checkedOptions = this.localStatuses.filter(el => el.isChecked);
      if (checkedOptions.length === 0) {
        return ('Статус претензии');
      }
      else if (checkedOptions.length>0 && checkedOptions.length <4) {
        return (checkedOptions.map(el => el.title).join(', '));
      } else if (checkedOptions.length === this.localStatuses.length){
        return (this.all.title);
      }
      else {
        return (checkedOptions.length + ' из ' + this.localStatuses.length + ' выбрано');
      }
      return this.localStatuses.filter(el => el.isChecked).map(el => el.title).join(', ');
    },
    isRealAllChecked() {
      console.log(this.localStatuses.every(el => el.isChecked));
      return this.localStatuses.every(el => el.isChecked);
    }
  },
  methods: {
    onSelect: function (option) {
      if (option.isChecked) {
        option.isChecked = false;

      } else {
        option.isChecked = true;
      }
    },
    selectAll: function() {
      this.localStatuses = this.localStatuses.map(el => {
        if (this.isAllChecked) {
          el.isChecked = true
        } else {
          el.isChecked = false
        }
        return el
      })
    },
    toggleClass: function() {
      this.isActive = !this.isActive
    },
  },
  watch: {
    isRealAllChecked(value) {
      this.isAllChecked = value
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
    color: #424141;
    margin: 0;
    padding: 0;
    font-family: Roboto;
    font-size: 17px;
    height: 22px;
    font-weight: bold;
    border: 1px solid #424141;
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
    border-left: 1px solid #424141;
    border-right: 1px solid #424141;
  }
  #dropdown-menu.open {
    display: block;
    cursor: pointer;
  }
  .open:last-child {
    border-bottom: 1px solid #424141;
  }
  ul#dropdown-menu.open:not(:last-child) {
  }
  li.dropdown-menu-option {
    border-bottom: 1px solid #d6d6d6;
    color: gray;
  }
  li.dropdown-menu-option:hover {
    color: #000000;
    background-color: #e2e2e2;
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
  .dropdown, .dropdown-menu-option > label {
    cursor: pointer;
  }



</style>
