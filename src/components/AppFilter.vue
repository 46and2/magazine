<template>
  <div class="filter">
    <div class="filter__controls">
      <button
        @click="filterOut"
        class="filter__button"
        type="button"
        title="Filter"
      ></button>
      <input
        v-model="searchTerm"
        @input="filterOut"
        class="filter__input"
        type="text"
        name="searchterm"
        id="searchterm"
        :placeholder="hint"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppFilter',
  props: {
    hint: {
      type: String,
      required: false,
      default: 'Filter'
    }
  },
  data() {
    return {
      searchTerm: ''
    };
  },
  methods: {
    filterOut() {
      this.$emit('filter', this.searchTerm);
    }
  }
};
</script>

<style>
.filter {
  display: flex;
  justify-content: center;
}

.filter__controls {
  display: flex;
  flex-basis: 100%;
}

.filter__button {
  width: 35px;
  height: 35px;
  background: #ffffff;
  background-image: url('../assets/img/search-solid.svg');
  background-size: 15px;
  background-position: center;
  background-repeat: no-repeat;
  border: 1px solid #d3dce8;
  border-radius: 3px 0 0 3px;
  cursor: pointer;
}

.filter__input {
  flex-grow: 1;
  padding: 5px 10px;
  border: 1px solid #d3dce8;
  border-left: none;
  border-radius: 0 3px 3px 0;
}

@media (min-width: 820px) {
  .filter__controls {
    flex-basis: calc((100% - 30px) / 3);
  }
}
</style>
