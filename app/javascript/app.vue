<template>
    <div id="app">
        <ul>
            <li v-for="memo in memos" :key="memo.id">
                {{ memo.title }}： {{ memo.description }}
            </li>
        </ul>
        <div>
            <input v-model="title" placeholder="title">
            <input v-model="description" placeholder="description">
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    data: function () {
        return {
            memos: "memos",
            title: '',
            description: ''
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
              color: whitesmoke;
          }
      }
      input, input:focus, input:active{
          outline: none;
          font-size: 2em;
          border: 2px solid #999;
          padding: .5ch 1ch;
          border-radius: 2ch;
      }
  }
</style>
