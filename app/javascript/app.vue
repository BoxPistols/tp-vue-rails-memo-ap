<template>
    <div id="app">
        <p>{{ memos }}</p>
    </div>
</template>

<script>
import { axios } from "axis";
export default {
    data: function () {
        return {
            memos: "memos",
        };
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

<style scoped>
  p {
      font-size: 2em;
      text-align: center;
  }
</style>
