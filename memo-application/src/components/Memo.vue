
<!--각각의 메모의 상태를 표현할 수 있는 컴포넌트-->
<template>
  <li class="memo-item">
  <!-- 2. 등록된 props 값을 각 DOM에 위치시킨다. -->
    <strong>{{ memo.title }}</strong>
    <template>{{ memo.content }}</template>
    <input type="text" ref="content" :value="memo.content">
    <button type="button" @click="deleteMemo"><i class="fas fa-times"></i></button>
  </li>
</template>

<script>
    export default {
        name: "Memo",
        //1. 부모에게 내려받은 props를 등록.
        props: {
            memo: {
                type: Object
            }
        },
        methods: {
            deleteMemo() {
                //부모로부터 props로 내려받은 memo의 id를 붑모 컴포넌트의 사용자 정의 이벤트인 deleteMemo 함수의 파라미터로 전달.
                const id = this.memo.id;
                this.$emit('deleteMemo', id);
            }
        }
    }
</script>

<style scoped>
.app-header {
  overflow: hidden;
  padding: 52px 0 27px;
}
.app-header h1 {
  float: left;
  font-size: 24px;
  text-align: center;
}
.memo-item {
  overflow: hidden;
  position: relative;
  margin-bottom: 20px;
  padding: 24px;
  box-shadow: 0 4px 10px -4px rgba(0,0,0,0.2);
  background-color: #fff;
  list-style: none;
}
.memo-item button {
  background: none;
  position: absolute;
  right: 20px;
  top: 20px;
  font-size: 20px;
  color: #e5e5e5;
  border: 0;
}
.memo-item strong {
  display: block;
  margin-bottom: 12px;
  font-size: 18px;
  font-weight: normal;
  word-break: break-all;
}
.memo-item p {
  margin: 0;
  font-size: 14px;
  line-height: 22px;
  color: #666;
}
.memo-item p input[type="text"] {
  box-sizing: border-box;
  width: 100%;
  font-size: inherit;
  border: 1px solid #999;
}

</style>
