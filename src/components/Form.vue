<template>
    <div>
    <h1>Form MEDDODS</h1>
     <form class="form" @submit.prevent="submitHandler">
        <div>
          <label for="name">Имя<span class="star">*</span></label>
          <input id="name" type="text" class="input" v-model.trim="name" placeholder="Имя">
          <small v-if="$v.name.$dirty && !$v.name.required"
          >Поле имя обязательное</small>
        </div>      
        <div>
          <label for="surname">Фамилия<span class="star">*</span></label>
          <input id="surname" type="text" class="input" v-model="surname" placeholder="Фамилия">
          <small v-if="$v.surname.$dirty && !$v.surname.required"
          >Поле Фамилия обязательное</small>
        </div>
        <div>
          <label id="patronymic">Отчество</label>
          <input id="patronymic" type="text" class="input" v-model="patronymic" placeholder="Отчество">
        </div>
        <div>
          <label for="birthday">Дата рождения<span class="star">*</span></label>
          <input id="birthday" type="date" class="input" v-model.number="birthday">
          <small v-if="$v.birthday.$dirty && !$v.birthday.required"
          >Поле Дата рождения обязательное</small>
        </div>
        <div>
          <label>Номер телефона</label>
          <input 
          type="tel" 
          required 
          @input="filterInput"
            placeholder="+7(555) 555-5555"
            autocomplete="tel"
          class="input" 
          v-model.number="phone">
        </div>
        <div>
          <label>Пол</label>
          <input type="text" class="input" v-model="gender" placeholder="Пол">
        </div>
        <div>
            <label for="groupClient">Группа клиентов</label>
            <select
                id="groupClient"
                v-model="groupClient"
                name="groupClient"
                multiple>
                <option>VIP</option>
                <option>Проблемные</option>
                <option>ОМС</option>
            </select>
        </div>
        <div>
            <label for="doctor">Лечащий врач</label>
            <select
                id="doctor"
                v-model="doctor"
                name="doctor"
                >
                <option>Иванов</option>
                <option>Захаров</option>
                <option>Чернышева</option>
            </select>
        </div>
        <div class="checkbox">
            <input id="checkbox" type="checkbox" v-model="sms" />
            <label for="checkbox">Не отправлять СМС</label>
        </div>
        <h2>Адрес</h2>
        <div>
          <label for="index">Индекс</label>
          <input id="index" type="text" class="input" v-model.number="index" placeholder="Индекс">
        </div>
        <div>
          <label for="country">Страна</label>
          <input id="country" type="text" class="input" v-model="country" placeholder="Страна">
        </div>
        <div>
          <label for="city">Город<span class="star">*</span></label>
          <input id="city" type="text" class="input" v-model="city" placeholder="Город">
          <small v-if="$v.city.$dirty && !$v.city.required"
          >Поле город обязательное</small>
        </div>
        <div>
          <label for="street">Улица</label>
          <input id="street" type="text" class="input" v-model="street" placeholder="Улица">
        </div>
        <div>
          <label for="house">Дом</label>
          <input id="house" type="text" class="input" v-model="house" placeholder="Дом">
        </div>
        <h2>Паспорт</h2>
        <div>
            <label for="passport">Тип документа<span class="star">*</span></label>
            <select
                id="passport"
                v-model="passport"
                name="passport"
                >
                <option>Паспорт</option>
                <option>Свидетельство о рождении</option>
                <option>Вод. удостоверение</option>
            </select>
            <small v-if="$v.passport.$dirty && !$v.passport.required"
          >Поле паспорт обязательное</small>
        </div>
        <div>
          <label for="series">Серия</label>
          <input id="series" type="number" class="input" v-model.number="series" placeholder="Серия">
        </div>
        <div>
          <label for="number">Номер</label>
          <input id="number" type="number" class="input" v-model.number="number" placeholder="Номер">
        </div>
        <div>
          <label for="issuedBy">Кем выдан</label>
          <input id="issuedBy" type="text" class="input" v-model="issuedBy" placeholder="Кем выдан">
        </div>
        <div>
          <label for="dateIssue">Дата выдачи<span class="star">*</span></label>
          <input id="dateIssue" type="date" class="input" v-model.number="dateIssue" placeholder="Дата выдачи">
          <small v-if="$v.dateIssue.$dirty && !$v.birthday.required"
          >Поле Дата выдачи обязательное</small>
        </div>
      <div>
        <h3><span class="star">*</span>Поле обязательное для заполнения.</h3>
        <button type="submit" class="button">
          Отправить
        </button>
      </div>
    </form>
    <div class="modal" v-if="modal" @close="modal = false">
        <div class="modal-content">
            <h3 slot="header">Клиент создан</h3>
            <button @click="modal = false">Закрыть</button>
        </div>
    </div>
  </div>
</template>


<script>
import {required} from 'vuelidate/lib/validators'

export default {
    data: () => ({
        modal: false,
        name: '',
        surname: '',
        patronymic: '',
        birthday: '',
        phone: '',
        gender: '',
        groupClient: [],
        doctor: '',
        sms: false,
        index: '',
        country: '',
        city: '',
        street: '',
        house: '',
        passport: '',
        series: '',
        number: '',
        issuedBy: '',
        dateIssue: '',
    }),
    validations: {
      name: { required },
      surname: { required }, 
      birthday: { required},
      city: { required },
      passport: { required },
      dateIssue: { required }
  },
  methods: {
      filterInput(e) {
        e.target.value = e.target.value.replace(/[^0-9]+/g, '')
      },
      submitHandler() {
          if (this.$v.$invalid) {
            this.$v.$touch()
            return;
          }
          this.modal = true
          const formData = {
            name: this.name,
            surname: this.surname,
            patronymic: this.patronymic,
            birthday: this.birthday,
            phone: this.phone,
            gender: this.gender,
            groupClient: this.groupClient,
            doctor: this.doctor,
            sms: this.sms,
            index: this.index,
            country: this.country,
            city: this.city,
            street: this.street,
            house: this.house,
            passport: this.passport
          }
          console.log(formData)
      }
  }

}
</script>

<style lang="scss">
    .form {
        border: 3px solid #000;
        margin: 10px auto;
        padding: 5px;
        width: 1000px;
        background-color: #e5e5e5;
    }

    .form > div {
        display: flex;
        flex-direction: column;
    }

    .checkbox {
        flex-direction: row !important;
        align-items: center;
    }

    .form label {
      font-size: 20px;
      font-weight: bold;
        text-align: left;
        margin-left: 5px;
        margin-top: 5px;
    }

    .form input {
        height: 30px;
        margin: 5px;
    }

    .form select {
        margin: 5px;
    }

    .form small {
        text-align: left;
        margin-left: 5px;
        color: red
    }

    .star {
      color:red;
    }

    .button {
      margin: 10px 50px;
      height: 30px;
      width: 300px;
      border: 2px solid #000;
      border-radius: 5px;;
      cursor: pointer;
      font-size: 16px;
      color: red;
      background-color:aquamarine;
    }

    .modal {
        position: fixed;
        z-index: 100;
        padding-top: 100px;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        overflow: auto;
        background-color: rgba(0,0,0,0.4);
    }
    .modal-content {
        background-color: #fefefe;
        margin: auto;
        padding: 20px;
        border: 1px solid #888;
        width: 80%;
    }
</style>