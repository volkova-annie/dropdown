<template>
  <div class='container' v-on-clickaway='close'>
    <button type="button" name="button" v-on:click='toggleClass' v-bind:class='[isActive ? "arrow" : "", "dropdown-menu-title"]'>
      <div class="placeholder">{{ placeholder }}</div>
    </button>
    <ul class='dropdown-menu' v-bind:class='{"open": isActive}'>
      <li class='dropdown-menu-item'>
        <label class='dropdown-menu-option'>
          <input class='dropdown-menu-option-input' type='checkbox' v-on:change='selectAll()' v-model='isAllChecked'/>{{options.allTitle}}
        </label>
      </li>
      <li class='dropdown-menu-item' v-for='option in localStatuses'>
        <label class='dropdown-menu-option'>
          <input class='dropdown-menu-option-input' type='checkbox' v-bind:value='option.value' v-model='option.isChecked'/>{{option.title}}
        </label>
      </li>
    </ul>
  </div>
</template>

<script>
import { directive as onClickaway } from 'vue-clickaway'

export default {
  directives: {
    onClickaway
  },
  props: ['options', 'statuses'],
  data: function () {
    return {
      isAllChecked: false,
      isActive: false,
      localStatuses: this.statuses.map(el => {
        return {
          ...el,
          isChecked: !!el.isChecked
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
    close: function() {
      this.isActive = false
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
  .dropdown-menu-title {
    width: 100%;
    position: relative;
    font-family: inherit;
    font-size: inherit;
    background-color: inherit;
    height: 22px;
    border: 1px solid #424141;
    text-align: left;
    cursor: pointer;
  }
  .dropdown-menu-title:after, .arrow:after {
    position: absolute;
    right: 15px;
    top: 3px;
    font-size: 14px;
  }
  .dropdown-menu-title:after {
    content: "▼";
  }
  .arrow:after {
    content: "▲";
  }
  .dropdown-menu-title:focus {
    outline: none;
  }
  .dropdown-menu {
    display: none;
    padding: 0;
    margin: 0;
    list-style: none;
    color: gray;
    border-left: 1px solid #424141;
    border-right: 1px solid #424141;
  }
  .dropdown-menu-item {
    display: block;
  }
  .open:last-child {
    border-bottom: 1px solid #424141;
  }
  .dropdown-menu.open {
    display: block;
  }
  .dropdown-menu-option {
    border-bottom: 1px solid #d6d6d6;
    display: block;
  }
  .dropdown-menu-option:hover {
    color: #000000;
    background-color: gray;
    cursor: pointer;
  }
  .dropdown-menu-option:last-child {
    border-bottom: none;
  }
  .dropdown-menu-option > li:hover {
    background-color: #e2e2e2;
  }
  .placeholder {
    padding-right: 25px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

</style>
