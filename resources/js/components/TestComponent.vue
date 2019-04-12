<style>
    body, input {
        font-family: Comic Sans;
        font-size: 14px;
        color: #0E610F;
    }

    table {
        width: 630px;
        margin: auto;
        border-radius: 3px;
        background-color: #fff;
    }

    th, td {
        min-width: 50px;
        padding: 10px 10px;
    }

    th {
        background-color: #0E610F;
        color: #ffffff;
        cursor: default;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    td {
        background-color: #f3f8f9;
    }

    .b20 {
        cursor: pointer;
        width: 30px;
        margin-left: 5px;
        text-align: center;
    }

    .th60 {
        width: 80px;
        margin: 0 calc(50% - 40px);
    }

    .th180 {
        width: 180px;
    }

    .thAm {
        font-weight: bold;
        border: 1px solid #a9a9a9;
        background-color: #f3f8f9;
    }
</style>
<template>
    <div>
        <div>
            <table>
                <thead>
                <tr>
                    <td colspan="9" style="text-align:right"><b>ОСТАТОК: </b><b>{{CalcPrice}}</b></td><!-- Итоговая сумма -->
                </tr>
                <tr>
                    <th>№</th>
                    <th>Наименование</th>
                    <th>Количество</th>
                    <th class="th60">Цена</th>
                    <th class="th60">Сумма</th>
                    <th>Действие</th>
                </tr>
                </thead>
                <tbody>

                <tr v-for="(item, val) in Data"> <!-- Цикл по строкам -->

                    <td style="text-align:center"><b>{{val + 1}}</b></td> <!-- Номер строки -->
                    <td><input class="th180" v-model="item['name']" placeholder="Введите наименование"
                               title="Введите наименование товара"></td> <!-- Наименование -->
                    <td><input class="th60" v-model="item['count']" type="number" min="0" max="999999"
                               maxlength="6" title="Введите количество товара"></td> <!-- Количество -->
                    <td><input class="th60" v-model="item['price']" type="number" min="0" max="999999"
                               maxlength="6" title="Введите цену товара"></td> <!-- Цена -->

                    <td><input class="th60 thAm" v-model="item['amount']" readonly title="Сумма за товар"></td> <!-- Сумма за товар -->

                    <td style="display: flex;">
                        <button class="b20" v-if="Data.length > 1" v-on:click="DeleteRow(val)" title="Удалить строку">del</button>
                        <!-- Удалить строку (если строк больше одной) -->
                        <button class="b20" v-if="Data.length >= 0" v-on:click="UpNumber(val)" title="Добавить кол-во">+</button>
                        <!-- Увеличить количество товара -->
                        <button class="b20" v-if="Data.length >= 0" v-on:click="DownNumber(val)" title="Добавить кол-во">-</button>
                        <!-- Уменьшить количество товара -->
                        <button class="b20" v-if="Data.length >= 0" v-on:click="ClearRow(val)" title="">х</button>
                        <!-- Очитить значения в строке -->
                    </td>
                </tr>
                </tbody>

                <tfoot>
                <tr>
                    <td colspan="9"><button class="b60" v-on:click="AddNewRow" title="Добавить строку в таблицу">Добавить поле</button></td>
                    <!-- Кнопка добавления стороки в таблицу -->
                </tr>
                </tfoot>
            </table>
        </div>
    </div>
</template>
<script>
    export default {
        data: function () {
            return {
                Data: [ // Массив строк
                    {name: '', count: 0, price: '', amount: ''}
                ]
            }
        },
        computed: { // Определяем вычисляемое свойство для автоматического пересчета сумм и итога
            CalcPrice: function () { // Расчёт сумм по строкам и общего остатка
                this.FullPrice = 70;
                for (var i = 0; i < this.Data.length; ++i) { // Цикл по строкам таблицы
                    this.Data[i].amount = this.Data[i].count * this.Data[i].price; // Расчёт суммы в строке
                    this.FullPrice = this.FullPrice - this.Data[i].amount; // Расчёт остатка средств
                }
                return this.FullPrice; // Функция возвращает остаток средств
            }
        },
        methods: {
            AddNewRow: function () { // Добавить новую строку в таблицу
                this.Data.push({name: '', count: 0, price: '', amount: ''});
            },
            DeleteRow: function (i) { // Удалить строку с номером i из таблицы
                this.Data.splice(i, 1);
            },
            UpNumber: function (i) { //Увеличить на +1 количество в строке с номером i
                this.Data[i].count++;
            },
            DownNumber: function (i) { //Уменьшить на +1 количество в строке с номером i
                this.Data[i].count--;
                if (this.Data[i].count < 0) {
                    alert('Значение не может быть отрицательным');
                }
            },
            ClearRow: function (i) {
                this.Data[i].name = '';
                this.Data[i].count = 0;
                this.Data[i].price = '';
                this.Data[i].amount = '';
            },
        },
    }
</script>

