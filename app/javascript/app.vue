<template>
    <div id="app">
        <ul>
            <li v-for="memo in memos" :key="memo.id">
                {{ memo.title }}： {{ memo.description }}
            </li>
        </ul>
    </div>
</template>

<script>
import axios from "axios";
export default {
    data: function () {
        return {
            memos: "memos",
        };
    },
    mounted() {
        this.setMemo();
    },
    methods: {
        setMemo: function () {
            axios
                .get("/api/memos")
                .then((response) => (this.memos = response.data));
        },
    },
};
</script>

<style scoped lang="scss">
  #app {
      width: 100%;
      display: flex;
      flex-direction: column;
      //   justify-content: center;
      align-items: center;
      ul {
          max-width: 60vw;
          margin: 10vh auto;
          li {
              font-size: 2em;
              color: tomato;
          }
      }
  }
</style>
