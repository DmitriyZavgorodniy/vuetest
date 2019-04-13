<template>
    <div>
        <header>
            <div class="container">
                <div><h1>НОВЫЙ САЙТ</h1></div>
            </div>
        </header>
        <section>
            <div class="row">
                <div class="col-md-2 side__bar" style="font-size: 20px;">
                    <router-link to="/HomePage">Главная</router-link>
                    <hr>
                    <router-link to="/PaymentPage">Заказ</router-link>
                </div>
                <div class="col-md-10">
                    <router-view></router-view>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Проверка')
        }
    }
</script>