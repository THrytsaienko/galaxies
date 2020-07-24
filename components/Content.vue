<template>
    <div class="content">
        <div class="content__container">
            <div class="content__header">
                <h1 class="content__title">Named galaxies</h1>
                <div class="content__search">
                    <img src="../assets/search.svg" alt="Search" class="content__icon" />
                    <input type="search" v-model="search" class="content__input" placeholder="Search galaxies">
                </div>
            </div>
            <div class="content__body">
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
            </div>
        </div>
    </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: "MainContent",
    data() {
      return {
        galaxies: [],
        sortDirection: 'ASC',
        search: ''
      }
    },
    computed: {
      sortedArray () {
        if(this.sortDirection === 'DESC') {
          return this.galaxies.slice().reverse().filter(galaxy => {
            return galaxy.name.toLowerCase().includes(this.search.toLowerCase());
          });
        } else {
          return this.galaxies.filter(galaxy => {
            return galaxy.name.toLowerCase().includes(this.search.toLowerCase());
          });
        }
      },
      addClass() {
        if(this.sortDirection === 'DESC') {
          return 'rotate'
        }
      }
    },
    mounted() {
      axios
        .get('https://cors-anywhere.herokuapp.com/https://test-frontend-api.herokuapp.com/galaxies')
        .then(response => {
          const sortedResponse = response.data.sort((a, b) => a.name.localeCompare(b.name));
          this.galaxies = sortedResponse;
        })
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

<style scoped lang="postcss">
.content {
    &__header {
         margin-bottom: 59px;
         max-width: 1010px;
         display: flex;
         justify-content: space-between;
    }

    &__title {
         font-family: Roboto;
         font-weight: 500;
         font-size: 34px;
         line-height: 40px;
         display: flex;
         align-items: center;
         letter-spacing: 0.25px;
         color: #263238;
    }

    &__input {
         width: 271px;
         border: 1px solid #e0e0e0;
         border-radius: 4px;
         padding: 10px 18px 10px 46px;
    }

    &__search {
         position: relative;
    }

    &__icon {
         position: absolute;
         width: 14px;
         height: 14px;
         top: 30%;
         left: 14px;
    }
}

.table {
    font-family: Roboto;

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
