<!--
import 구문은 추출된 자바스크립트의 모듈을 불러오는 문법. 다만 모든 멤버를 받아오기 위한
전제조건으로 해당하는 모듈에서 default 파라미터를 통해 모듈을 내보내야함.

export 구문은 javascript 모듈을 내보낼 때 사용.
모듈을 내보낼때는 default 파라미터를 입력해주는 방법과 변수 이름으로 내보내기가 있다.
-->



<template>
    <div class="app-header">
      <h1>메모 애플리케이션</h1>
    </div>
</template>

<script>
    export default {
        name: "AppHeader"
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
</style>
