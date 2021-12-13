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
      <ul>
        <li><check-box label="ラジオ体操" v-model="checkedTasks"/></li>
        <li><check-box label="マイレージログイン" v-model="checkedTasks"/></li>
        <li><check-box label="たぬきショッピング日替りCheck" v-model="checkedTasks"/></li>
        <li><check-box label="リサイクルBOX" v-model="checkedTasks"/></li>
      </ul>
    </div>
    <div class="panel-naked">
      <ul>
        <li><check-box label="海岸のボトルレシピ" v-model="checkedTasks"/></li>
        <li>
          <span>住民レシピ</span>&nbsp;
          <check-box label="1st" slim v-model="checkedTasks"/>&nbsp;
          <check-box label="2nd" slim v-model="checkedTasks"/>&nbsp;
          <check-box label="3rd" slim v-model="checkedTasks"/>
        </li>
      </ul>
    </div>
    <div class="flex frex-row justify-around space-x-1">
      <div class="panel">
        <h2 class="panel-header">博物館</h2>
        <ul>
          <li><check-box label="ハトの巣" v-model="checkedTasks"/></li>
          <li><check-box label="化石の鑑定" v-model="checkedTasks"/></li>
        </ul>
      </div>
      <div class="panel">
        <h2 class="panel-header">たぬき商店</h2>
        <ul>
          <li><check-box label="カブ価チェック" v-model="checkedTasks"/></li>
          <li><check-box label="商品チェック" v-model="checkedTasks"/></li>
          <li><check-box label="カベ・床" v-model="checkedTasks"/></li>
        </ul>
      </div>
    </div>
    <div class="panel-naked">
      <ul>
        <li><check-box label="仕立て屋チェック" v-model="checkedTasks"/></li>
        <li><check-box label="かっぺいツアー" v-model="checkedTasks"/></li>
        <li>
          <span>訪問者</span>&nbsp;
          <check-box label="昼" v-model="checkedTasks"/>
          &nbsp;
          <check-box label="夜" v-model="checkedTasks"/>
        </li>
      </ul>
    </div>
    <div class="flex flex-row justify-around space-x-1">
      <Panel header="月曜">
        <ul><li><check-box label="パニー島" slim v-model="checkedTasks"/></li></ul>
      </Panel>
      <Panel header="土曜">
        <ul>
          <li><check-box label="とたけけ" slim v-model="checkedTasks"/></li>
        </ul>
      </Panel>
      <Panel header="日曜">
        <ul>
          <li><check-box label="ウリ" slim v-model="checkedTasks"/></li>
          <li><check-box label="フェス" slim v-model="checkedTasks"/></li>
        </ul>
      </Panel>
    </div>
    <Panel header="ハッピーホームデザイナー">
      <ul>
          <li><check-box label="海岸のボトルレシピ" v-model="checkedTasks"/></li>
          <li><check-box label="レストランでレシピ" v-model="checkedTasks"/></li>
          <li><check-box label="ポキ家具日替りチェック" v-model="checkedTasks"/></li>
          <li><check-box label="お取り寄せ(最大5回)" v-model="checkedTasks"/></li>
        </ul>
    </Panel>
    <div class="panel-naked">
      <ul>
          <li><check-box label="ゆきだるま(冬季限定)" v-model="checkedTasks"/></li>
          <li><check-box label="木材採取" v-model="checkedTasks"/></li>
          <li><check-box label="石コツコツ" v-model="checkedTasks"/></li>
          <li><check-box label="水やり" v-model="checkedTasks"/></li>
          <li><check-box label="ラコスケにホタテ" v-model="checkedTasks"/></li>
      </ul>
    </div>
  </div>
  
</div>
</template>

<script>
import CheckBox from "./components/CheckBox.vue"
import Panel from "./components/Panel.vue"
import {computed, reactive} from "vue"


export default {
  name: 'App',
  components: {
    CheckBox,
    Panel
  },
  setup() {
    //localStorageから最後の状態を取得
    let initialTasks;
    let st = localStorage;
    const ST_KEY = "checked_tasks";
    try {
      initialTasks = st.getItem(ST_KEY);
      if (initialTasks == null) {
        initialTasks = [];
      } else {
        initialTasks = JSON.parse(initialTasks);
      }
    } catch {
      //例外を吐いたらまっさらな状態とみなして進める。
      initialTasks = [];
    }

    //ただの配列でもいいかと思って実装したら、チェックイベントが親に伝播した時に望ましい値が保存されなくなってしまった。
    //reactiveは値が変わった瞬間に当オブジェクトを利用しているコンポーネントへ値を瞬時に反映させているため、
    //この実装でないと、現在のタスク一覧がうまくリンクしない。
    let checkedTasksInner = reactive({value: initialTasks});

    //TODO 達成カウント
    const onClickResetBtn = () => {
      document.querySelectorAll("input[type='checkbox']").forEach((val) => {
        val.checked = false;
      });
      st.setItem(ST_KEY, JSON.stringify([]));
    };

    let checkedTasks = computed({
      get: () => checkedTasksInner.value,
      set: (callBackArray) => {
        checkedTasksInner.value = callBackArray;
        st.setItem(ST_KEY, JSON.stringify(callBackArray));
      }
    });

    return {
      checkedTasks,
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
  @apply border border-gray-400 rounded p-2 flex-1;
  margin: 0.8rem 0 0.25rem 0;
}
.panel-header {
  @apply bg-white px-4 rounded;
  width: fit-content;
  margin-top: -18px;
}
.panel ul {
  @apply mt-2;
}
.panel-naked {
  @apply px-2 py-1 border border-transparent;
}
.inbox {
  background-color: #e7f3d9;
  @apply rounded p-4;
}
</style>
