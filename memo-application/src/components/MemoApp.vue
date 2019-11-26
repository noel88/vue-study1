<!--메모들의 상태를 관리하는 컴포넌트-->
<template>
    <div class="memo-app">
<!--      <memo-form v-on:addMemo="addMemo"></memo-form> 아래 코드와 같은 의미-->
      <memo-form @addMemo="addMemo"></memo-form>
      <ul class="memo-list">
        <memo v-for="memo in memos" :key="memo.id" :memo="memo" @deleteMemo="deleteMemo" @updateMemo="updateMemo"></memo>
      </ul>
    </div>
</template>

<script>
    import MemoForm from "./MemoForm";
    import Memo from "./Memo";
    export default {
        name: "MemoApp",
        components: {Memo, MemoForm},
        data() {
            return {
                memos: [],
            }
        },
        created() {
            //1. 만약 기존에 추가된 loocalStorage에 데이터가 있다면 created 훅에서 localStorage의 데이터 컴포넌트 내의 memos 데이터에 넣어주고 그렇지 않다면 빈 배열로 초기화.
            this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
        },
        methods: {
            addMemo(payload) {
                //MemoForm에서 올려 받은 데이터를 먼저 컴포넌트 내부 데이터에 추가
                this.memos.push(payload);
                //내부 데이터를 변환 후, 로컬 스토리지에 저장.
                this.storeMemo();
            },
            storeMemo() {
                const memosToString = JSON.stringify(this.memos);
                localStorage.setItem('memos', memosToString);
            },
            deleteMemo(id) {
                //1. 자식 컴포넌트에서 인자로 전달해주는 id에 해당하는 메모 데이터의 인덱스를 찾는다.
                const targetIndex = this.memos.findIndex(v => v.id === id);
                //2. 찾은 인덱스 번호에 해당하는 메모 데이터를 삭제.
                this.memos.splice(targetIndex, 1);
                //3.삭제된 후의 데이터를 다시 로컬스토리지에 마찬가지로 저장.
                this.storeMemo();
            },
            updateMemo(payload) {
                //1.수정된 메모를 저장한다.
                const { id, content } = payload;
                const targetIndex = this.memos.findIndex(v => v.id === id);
                const targetMemo = this.memos[targetIndex];
                this.memos.splice(targetIndex, 1, { ...targetMemo, content});
                this.storeMemo();
            }
        }
    }
    // 컴포넌트의 초기화에 필요한 데이터를 외부 애플리케이션에 요청해서 받아와야 하는 경우에는 일반적으로 훅의 실행 타이밍이 가장 빠른 crated훅에서 데이터를 받아옴.
</script>

<style scoped>
.memo-list {
  padding: 20px 0;
  margin: 0;
}
</style>
