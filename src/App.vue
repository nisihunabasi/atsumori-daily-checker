<template>
<div class="container md:container mx-auto px-3 bg-container pt-1 pb-4">
  <h1 class="text-center border-b border-gray-400 py-2 mb-4 font-bold">
    あつ森デイリーチェッカー
  </h1>
  <div class="inbox">
    <div class="mb-6">
      <button class="btn-default" @click="onClickResetBtn">リセット</button>
    </div>
    <div class="panel">
      <h2 class="panel-header">役場</h2>
      <ul class="mt-3">
        <li>
          <label>
            <input type="checkbox">
            &nbsp;ラジオ体操
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox">
            &nbsp;マイレージログイン
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox">
            &nbsp;たぬきショッピング日替りCheck
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox">
            &nbsp;リサイクルBOX
          </label>
        </li>
      </ul>
    </div>
    <div class="panel-naked">
      <ul>
        <li>
          <label>
            <input type="checkbox">
            &nbsp;海岸のボトルレシピ
          </label>
        </li>
        <li>
          <span>住民レシピ</span>&nbsp;
          <label>
            <input type="checkbox">
            10日
          </label>
          &nbsp;
          <label>
            <input type="checkbox">
            20日
          </label>
          &nbsp;
          <label>
            <input type="checkbox">
            30日
          </label>
        </li>
      </ul>
    </div>
    <div class="flex frex-row justify-around">
      <div class="panel">
        <h2 class="panel-header">博物館</h2>
        <ul class="mt-3">
          <li>
            <label>
              <input type="checkbox">
              &nbsp;ハトの巣
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox">
              &nbsp;化石の鑑定
            </label>
          </li>
        </ul>
      </div>
      <div class="panel">
        <h2 class="panel-header">たぬき商店</h2>
        <ul class="mt-3">
          <li>
            <label>
              <input type="checkbox">
              &nbsp;カブ価チェック
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox">
              &nbsp;商品チェック
            </label>
          </li>
          <li>
            <label>
              <input type="checkbox">
              &nbsp;カベ・床
            </label>
          </li>
        </ul>
      </div>
    </div>
    <div class="panel-naked">
      <ul>
        <li>
          <label>
            <input type="checkbox">
            &nbsp;仕立て屋チェック
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox">
            &nbsp;かっぺいツアー
          </label>
        </li>
        <li>
          <span>訪問者</span>&nbsp;
          <label>
            <input type="checkbox">
            昼
          </label>
          &nbsp;
          <label>
            <input type="checkbox">
            夜
          </label>
        </li>
      </ul>
    </div>
  </div>
  
</div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  setup() {
    //TODO 達成カウント
    const onClickResetBtn = () => {
      document.querySelectorAll("input[type='checkbox']").forEach((val) => {
        val.checked = false;
      });
    };
    return {
      onClickResetBtn
    };
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*color: #2c3e50;*/
  color: #333;
  background-color: #87c13f;
}
.btn-default {
  @apply bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded inline-flex border border-gray-400 items-center focus:outline-none focus:ring-2 focus:ring-gray-900 my-2;
}
.btn-default:active {
  @apply bg-gray-400;
}
.panel {
  @apply border border-gray-400 rounded p-4;
  margin: 0.8rem 0 0.5rem 0;
}
.panel-header {
  @apply bg-white px-4 rounded;
  width: fit-content;
  margin-top: -26px;
}
.panel-naked {
  @apply p-4 border border-transparent;
}
.inbox {
  background-color: #e7f3d9;
  @apply rounded p-4;
}
</style>
