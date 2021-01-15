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
            <button @click="addMemo">メモを追加</button>
            <!-- TODO -->
            <!-- <button @click="rmMemo">メモを削除</button> -->
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
        setMemo() {
            axios
                .get("/api/memos")
                .then((res) => (this.memos = res.data));
        },
        addMemo(){
            axios.post('/api/memos',{
                title: this.title,
                description: this.description,
            })
            .then(res => {
                this.setMemo();
            })
            .catch(err => {
                console.error(err);
            })
        },
        //  TODO
        // rmMemo(){
        //     axios.delete("/api/memos", {data: {id: memos.id}})
        //     .then(res => {
        //         this.setMemo();
        //     })
        //     .catch(err => {
        //         console.error(err);
        //     })
        // },
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
      input, input:focus, input:active, button{
          outline: none;
          font-size: 2em;
          border: 2px solid #999;
          padding: .5ch 1ch;
          border-radius: 2ch;

      }
  }
</style>
