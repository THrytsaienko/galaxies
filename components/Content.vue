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
              <div v-if="loading">Loading...</div>
              <Table v-else
                     :dataToRender="this.galaxies"
                     :wordToSearch="this.search" />
            </div>
        </div>
    </div>
</template>

<script>
  import Table from '~/components/Table.vue';
  import axios from 'axios';

  export default {
    name: "MainContent",
    data() {
      return {
        galaxies: [],
        search: '',
        loading: true
      }
    },
    components: {
      Table
    },
    mounted() {
      axios
        .get('https://cors-anywhere.herokuapp.com/https://test-frontend-api.herokuapp.com/galaxies')
        .then(response => {
          const sortedResponse = response.data.sort((a, b) => a.name.localeCompare(b.name));
          this.galaxies = sortedResponse;
          this.loading = false;
        })
    }
  }
</script>

<style scoped lang="scss">
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
</style>
