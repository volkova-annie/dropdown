<template>
  <div class='container'>
    <button type="button" name="button" v-on:click='toggleClass' v-bind:class='[isActive ? "arrow" : "", "dropdown-menu-title"]'>
      <span class="placeholder">{{ placeholder }}</span>
    </button>
    <ul id='dropdown-menu' v-bind:class='{"open": isActive}'>
      <label>
        <li class='dropdown-menu-option' >
          <input class='dropdown' type='checkbox' v-on:change='selectAll()' v-model='isAllChecked'/>{{options.allTitle}}
        </li>
      </label>
      <label class='dropdown-menu-option' v-for='option in localStatuses'>
        <li>
          <input class='dropdown' type='checkbox' v-bind:value='option.value' v-model='option.isChecked'/>{{option.title}}
        </li>
      </label>
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
      localStatuses: this.statuses.map(el => {
        return {
          ...el,
          isChecked: false
        }
      })
    }
  },
  computed: {
    placeholder() {
      const checkedOptions = this.localStatuses.filter(el => el.isChecked);

      if (checkedOptions.length === 0) {
        return this.options.placeholder;
      }

      if (checkedOptions.length < 4) {
        return checkedOptions.map(el => el.title).join(', ');
      }

      if (checkedOptions.length === this.localStatuses.length){
        return this.options.allTitle;
      }

      return checkedOptions.length + ' из ' + this.localStatuses.length + ' выбрано';
    },
    isRealAllChecked() {
      console.log(this.localStatuses.every(el => el.isChecked));
      return this.localStatuses.every(el => el.isChecked);
    }
  },
  methods: {
    selectAll: function() {
      this.localStatuses.map(el => {
        if (this.isAllChecked) {
          el.isChecked = true;
        } else {
          el.isChecked = false;
        }
        return el
      })
    },
    toggleClass: function() {
      this.isActive = !this.isActive;
    },
  },
  watch: {
    isRealAllChecked(value) {
      this.isAllChecked = value;
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
    width: 82%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .dropdown, .dropdown-menu-option > label {
    cursor: pointer;
  }
</style>
