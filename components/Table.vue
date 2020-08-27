<template>
  <div class="table">
    <div class="table__header">
      <div class="table__head table__head--name" @click="changeSort">
        <p>Galaxy name</p>
        <img class="table__icon" src="../assets/arrow.svg" alt="Arrow"
             :class="addClass">
      </div>
      <div class="table__head table__head--constellation">Constellation</div>
      <div class="table__head table__head--origin">Origin of name</div>
    </div>
    <div v-for="item in sortedArray" :key="item.id" class="table__row">
      <div class="table__cell table__name">
        <div class="table__image-block">
          <img :src="item.img" alt="Galaxy" class="table__image">
        </div>
        <p>{{item.name}}</p>
      </div>
      <div class="table__cell table__constellation">{{item.constellation}}</div>
      <div class="table__cell table__origin">{{item.originOfName}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Table",
  data() {
    return {
      sortDirection: 'ASC'
    }
  },
  props: {
    dataToRender: Array,
    wordToSearch: String
  },
  computed: {
    sortedArray () {
      if(this.sortDirection === 'DESC') {
        return this.dataToRender.slice().reverse().filter(galaxy => {
          return galaxy.name.toLowerCase().includes(this.wordToSearch.toLowerCase());
        });
      } else {
        return this.dataToRender.filter(galaxy => {
          return galaxy.name.toLowerCase().includes(this.wordToSearch.toLowerCase());
        });
      }
    },
    addClass() {
      if(this.sortDirection === 'DESC') {
        return 'rotate'
      }
    }
  },
  methods: {
    changeSort() {
      if (this.sortDirection === 'ASC') {
        this.sortDirection = 'DESC';
      } else {
        this.sortDirection = 'ASC';
      }
    }
  }
}
</script>

<style scoped lang="scss">
.table {
  font-family: Roboto, sans-serif;

  &__head {
    margin-bottom: 15px;
    font-size: 12px;
    line-height: 14px;
    letter-spacing: 1px;
    text-transform: uppercase;
    color: #909597;

    &--name {
      width: 270px;
      color: #263238;
      display: flex;
      cursor: pointer;
      font-weight: 900;
    }

    &--constellation {
      width: 200px;
    }

    &--origin {
      width: 540px;
    }
  }

  &__header {
    display: flex;
  }

  &__row {
    display: flex;
    max-width: 1010px;
    border-top: 1px solid #E0E0E0;

    &:last-child {
      border-bottom: 1px solid #E0E0E0;
    }
  }

  &__cell {
    font-size: 16px;
    line-height: 24px;
    border-bottom: none;
    border-right: none;
    color: #263238;
    font-weight: 300;
    color: #263238;
    display: flex;
    align-items: center;
    border-left: 1px solid #E0E0E0;

    &:last-child {
      border-right: 1px solid #E0E0E0;
    }
  }

  &__name {
    padding: 17px 20px;
    display: flex;
    width: 270px;
    font-weight: 500;
  }

  &__icon {
    width: 11px;
    height: 11px;
    margin-left: 10px;
    transition: .4s;

    &.rotate {
      transform: rotateX(180deg);
    }
  }

  &__image-block {
    width: 30px;
    height: 30px;
    margin-right: 21px;
  }

  &__image {
    width: 100%;
    height: 100%;
  }

  &__constellation,
  &__origin {
    padding: 17px 15px;
  }

  &__constellation {
    width: 200px;
  }

  &__origin {
    width: 540px;
  }
}
</style>
