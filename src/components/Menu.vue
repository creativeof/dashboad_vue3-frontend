<template>
  <nav id="sidebarMenu" class="col-md-3 col-lg-2 d-md-block bg-light sidebar collapse">
    <div class="position-sticky pt-3">
      <ul class="nav flex-column">
        <li class="nav-item">
          <router-link to="/" exact-active-class="active" class="nav-link">
            ダッシュボード
          </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/users" active-class="active" class="nav-link">
            ユーザー
          </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/roles" active-class="active" class="nav-link">
            権限
          </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/products" active-class="active" class="nav-link">
            商品
          </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/orders" active-class="active" class="nav-link">
            注文
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Menu"
}
</script>
