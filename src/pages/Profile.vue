<template>
  <div>
    <h3>アカウント情報</h3>
    <form @submit.prevent="infoSubmit">
      <div class="mb-3">
        <label>姓</label>
        <input v-model="infoData.first_name" class="form-control" name="first_name">
      </div>
      <div class="mb-3">
        <label>名</label>
        <input v-model="infoData.last_name" class="form-control" name="last_name">
      </div>
      <div class="mb-3">
        <label>メールアドレス</label>
        <input v-model="infoData.email" class="form-control" name="email">
      </div>

      <button class="btn btn-outline-secondary">保存</button>
    </form>

    <h3 class="mt-4">パスワード変更</h3>
    <form @submit.prevent="passwordSubmit">
      <div class="mb-3">
        <label>パスワード</label>
        <input v-model="passwordData.password" type="password" class="form-control" name="password">
      </div>
      <div class="mb-3">
        <label>パスワード確認</label>
        <input v-model="passwordData.password_confirm" type="password" class="form-control" name="password_confirm">
      </div>

      <button class="btn btn-outline-secondary">保存</button>
    </form>
  </div>
</template>

<script lang="ts">
import {reactive, computed, watch} from 'vue';
import axios from 'axios';
import {useStore} from 'vuex';

export default {
  name: "Profile",
  setup() {
    const infoData = reactive({
      first_name: '',
      last_name: '',
      email: ''
    });
    const passwordData = reactive({
      password: '',
      password_confirm: ''
    })

    const store = useStore();
    const user = computed(() => store.state.User.user);

    watch(user, () => {
      infoData.first_name = user.value.first_name;
      infoData.last_name = user.value.last_name;
      infoData.email = user.value.email;
    });

    const infoSubmit = async () => {
      console.log(infoData);
      const {data} = await axios.put('users/info', infoData);
      await store.dispatch('User/setUser', data);
    }
    const passwordSubmit = async () => {
      await axios.put('users/password', passwordData);
    }

    return {
      infoData,
      passwordData,
      infoSubmit,
      passwordSubmit
    }
  }
}
</script>
