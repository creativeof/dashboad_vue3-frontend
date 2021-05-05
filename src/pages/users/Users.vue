<template>
  <div>
    <div class="pt-3 pb-2 mb-3 border-bottom">
      <router-link to="/users/create" class="btn btn-sm btn-outline-secondary">追加</router-link>
    </div>

    <div class="table-responsive">
      <table class="table table-striped table-sm">
        <thead>
          <tr>
            <th>#</th>
            <th>名前</th>
            <th>メーアドレス</th>
            <th>権限</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.first_name }} {{ user.last_name }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.role.name }}</td>
            <td>
              <div class="btn-group mr-2">
                <router-link :to="`/users/${user.id}/edit`" class="btn btn-sm btn-outline-secondary">編集</router-link>
                <a href="javascript:void(0)" class="btn btn-sm btn-outline-secondary" @click="del(user.id)">削除</a>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <Paginator :last-page="lastPage" @page-changed="load($event)"/>
  </div>
</template>

<script lang="ts">
import {onMounted, ref} from 'vue'
import axios from 'axios'
import {User} from '../../models/user'
import Paginator from '../../components/Paginator.vue'

export default {
  name: "Users",
  components: {Paginator},

  setup() {
    const users = ref([]);
    const lastPage = ref(0);

    const load = async (page = 1) => {
      const {data} = await axios.get(`users?page=${page}`);
      users.value = data.data;
      lastPage.value = data.meta.last_page;
    };

    onMounted(load);

    const del = async (id: number) => {
      if (confirm('Are you sure?')) {
        await axios.delete(`users/${id}`);
        users.value = users.value.filter((u: User) => u.id !== id);
      }
    }

    return {
      users,
      lastPage,
      del,
      load
    }
  }
}
</script>
