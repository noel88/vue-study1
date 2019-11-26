<!--사용자의 메모를 입력받는 폼 컴포넌트-->
<template>
    <div class="memo-form">
      <form @submit.prevent="addMemo">
        <fieldset>
          <div>
            <input type="text" class="memo-form__title-form" placeholder="메모의 제목을 입력해주세요." v-model="title">
            <textarea class="memo-form__content-form" placeholder="메모의 내용을 입력해주세요." v-model="content"></textarea>
            <button type="reset"><i class="fas fa-sync-alt"></i></button>
          </div>
          <button type="submit">등록하기</button>
        </fieldset>
      </form>
    </div>
</template>

<script>
    export default {
        name: "MemoForm",
        data() {
            return {
                //사용자가 입력할 제목과 콘텐츠가 저장될 데이터의 키와 값
                title: '',
                content: '',
                //v-model 디렉티브를 통해 모델을 연동하면 사용자가 입력 필드에 값을 입력할 때 v-model을 통해 데이터 바인딩 되어있는 모델 변수도 함께 갱신.
            }
        },
        methods: {
            resetFields() {
                this.title = '';
                this.content = '';
            },
            addMemo() {
                //비구조화 할당 구문을 이용하여 변수를 선언한다. - 객체의 속성을 해제하여 그 값을 각각의 변수에 담을 수 있도록 하는 자바스크립트 표현식 문법.
                const { title, content } = this;
                //데이터의 고유한 식별자를 생성.
                const id = new Date().getTime();

                //제목이나 내용을 입력하지 않는 경우를 대비하여 방어 코드를 추가
                const isEmpty = title.length <= 0 || content.length <= 0;
                if (isEmpty) {return false;}
                //addMemo 이벤트를 발생시키고 payload로 사용자가 입력한 데이터를 넣어준다.
                this.$emit('addMemo', {id, title, content});
                //부모 컴포넌트에 데이터를 전파한 후 데이터를 다시 원상태로 초기화.
                this.resetFields();
            }
        }
    }
</script>

<style scoped>
.memo-form {
  margin-bottom: 24px;
  padding-bottom: 40px;
  border-bottom: 1px solid #eee;
}
.memo-form form fieldset div {
  position: relative;
  padding: 24px;
  margin-bottom: 20px;
  box-shadow: 0 4px 10px -4px rgba(0,0,0,0.2);
  background-color: #ffffff;
}
.memo-form form fieldset div button {
  position: absolute;
  right: 20px;
  bottom: 20px;
  font-size: 16px;
  background: none;
}
.memo-form form fieldset button[type="submit"] {
  float: right;
  width: 96px;
  padding: 12px 0;
  border-radius: 4px;
  background-color: #ff5a00;
  color: #fff;
  font-size: 16px;
}
.memo-form form fieldset .memo-form__title-form {
  width: 100%;
  margin-bottom: 12px;
  font-size: 18px;
  line-height: 26px;
}
.memo-form form fieldset .memo-form__content-form {
  width: 100%;
  height: 66px;
  font-size: 14px;
  line-height: 22px;
  vertical-align: top;
}
.memo-form input:focus {
  outline: none;
}
</style>
