<template>
<ul class="nav nav-pills mb-3 justify-content-center" id="pills-tab" role="tablist">
    <li class="nav-item" role="presentation">
        <router-link :to="{name:'home'}">
            <button class="nav-link active" id="pills-home-tab" data-bs-toggle="pill" data-bs-target="#pills-home" type="button"
                role="tab" aria-controls="#pills-router-link" aria-selected="true">
                Калькулятор
            </button>
        </router-link>
    </li>
    <li class="nav-item" role="presentation">
        <router-link :to="{name:'exchange'}">
            <button class="nav-link" id="pills-profile-tab" data-bs-toggle="pill" data-bs-target="#pills-profile" type="button"
                role="tab" aria-controls="#pills-profile" aria-selected="false">
                Обменный курс
            </button>
        </router-link>
    </li>
</ul>
</template>

<script>
export default {

}
</script>

<style>
    .nav a{
        text-decoration: none;
    }
</style>