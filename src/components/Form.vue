<template>
    <div>
    <h1>Form MEDODS</h1>
     <form class="form" @submit.prevent="submitHandler">
        <h2>Данные клиента</h2>
        <div class="form__field">
          <label for="surname">Фамилия<span class="star">*</span></label>
          <input id="surname" type="text" class="input" v-model="surname" placeholder="Маметьев">
          <small v-if="$v.surname.$dirty && !$v.surname.required"
          >Поле Фамилия обязательное</small>
        </div>
        <div class="form__field">
          <label for="name">Имя<span class="star">*</span></label>
          <input id="name" type="text" v-model.trim="name" placeholder="Илья">
          <small v-if="$v.name.$dirty && !$v.name.required"
            >Поле Имя обязательное</small>
        </div>      
        <div class="form__field">
          <label id="patronymic">Отчество</label>
          <input id="patronymic" type="text" class="input" v-model="patronymic" placeholder="Сергеевич">
        </div>
        <div class="form__field">
          <label for="birthday">Дата рождения<span class="star">*</span></label>
          <input id="birthday" type="date" class="input" v-model="birthday">
          <small v-if="$v.birthday.$dirty && !$v.birthday.required"
          >Поле Дата рождения обязательное</small>
        </div>
        <div class="form__field">
          <label>Номер телефона</label>
          <input 
          @input="filterNumber"
          type="tel"
          class="input" 
          v-model.number="phone">
        </div>
        <div class="form__field">
          <label for="gender">Пол</label>
          <select
                id="gender"
                v-model="gender"
                name="gender">
                <option>Мужской</option>
                <option>Женский</option>
            </select>
        </div>
        <div class="form__field">
            <label for="groupClient">Группа клиентов</label>
            <select
                id="groupClient"
                class="groupClient"
                v-model="groupClient"
                name="groupClient"
                multiple>
                <option>VIP</option>
                <option>Проблемные</option>
                <option>ОМС</option>
            </select>
        </div>
        <div class="form__field">
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
        <div class="form__field class form__field--checkbox">
            <input id="checkbox" type="checkbox" v-model="sms" />
            <label for="checkbox">Не отправлять СМС</label>
        </div>
        <h2>Адрес</h2>
        <div class="row">
          <div class="form__field form__field--index">
            <label for="index">Индекс</label>
            <input id="index" type="text" class="input" v-model.number="index" placeholder="123456">
          </div>
          <div class="form__field form__field--country">
            <label for="country">Страна</label>
            <input id="country" type="text" class="input" v-model="country" placeholder="Российская Федерация">
          </div>
        </div>
        <div class="form__field">
          <label for="region">Область</label>
          <input id="region" type="text" class="input" v-model="region" placeholder="Челябинская">
        </div>
        <div class="form__field">
          <label for="city">Город<span class="star">*</span></label>
          <input id="city" type="text" class="input" v-model="city" placeholder="Магнитогорск">
          <small v-if="$v.city.$dirty && !$v.city.required"
          >Поле Город обязательное</small>
        </div>
        <div class="row">
          <div class="form__field form__field--street">
            <label for="street">Улица</label>
            <input id="street" type="text" class="input" v-model="street" placeholder="Ленина">
          </div>
          <div class="form__field form__field--house">
            <label for="house">Дом</label>
            <input id="house" type="text" class="input " v-model="house" placeholder="123a">
          </div>
        </div>
        <h2>Паспорт</h2>
        <div class="form__field">
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
          >Поле Тип документа обязательное</small>
        </div>
        <div class="row row--passport">
          <div class="form__field">
            <label for="series">Серия</label>
            <input id="series" type="number" class="input" v-model.number="series" placeholder="7410">
            <small v-if="$v.series.$dirty && (!$v.series.minLength || !$v.series.maxLength)"
            >Серия должна быть из {{$v.series.$params.minLength.min}} 
            цифр, сейчас у вас {{this.series.toString().length}}</small>
          </div>
          <div class="form__field">
            <label for="number">Номер</label>
            <input id="number" type="number" class="input" v-model.number="number" placeholder="646387">
            <small v-if="$v.number.$dirty && (!$v.number.minLength || !$v.number.maxLength)"
            >Номер должнен быть из {{$v.number.$params.minLength.min}} 
            цифр,  сейчас у вас {{this.number.toString().length}}</small>
          </div>
        </div>
        <div class="form__field">
          <label for="issuedBy">Кем выдан</label>
          <input id="issuedBy" type="text" class="input" v-model="issuedBy" placeholder="Кем выдан">
        </div>
        <div class="form__field">
          <label for="dateIssue">Дата выдачи<span class="star">*</span></label>
          <input id="dateIssue" type="date" class="input" v-model="dateIssue" placeholder="Дата выдачи">
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
            <button class="button" @click="modal = false">Закрыть</button>
        </div>
    </div>
  </div>
</template>


<script>
import {required, minLength , maxLength} from 'vuelidate/lib/validators'

export default {
    data: () => ({
        modal: false,
        name: '',
        surname: '',
        patronymic: '',
        birthday: '',
        phone: '7',
        gender: '',
        groupClient: [],
        doctor: '',
        sms: false,
        index: '',
        country: '',
        region: '',
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
      dateIssue: { required },
      series: { minLength: minLength(4), maxLength: maxLength(4) },
      number: { minLength: minLength(6), maxLength: maxLength(6) }
    },
  filters: {
    phoneFilter(phone) {
      return phone
        .replace(/[^0-9]/g, '')
        .replace(/(\d{3})(\d{3})(\d{4})/, '($1) $2-$3')
    }
  },
  methods: {
      submitHandler() {
          if (this.$v.$invalid) {
            this.$v.$touch()
            return;
          }
          this.modal = true
      }
  }

}
</script>

<style lang="scss">
  .form {
    border: 3px solid #000;
    margin: 10px auto;
    padding: 15px;
    background-color: #e5e5e5;

    .form__field {
      display: flex;
      flex-direction: column;
    }

    .form__field--checkbox {
      flex-direction: row;
      align-items: center;

      input {
        width: 20px;
      }
    }

    label {
      font-size: 20px;
      font-weight: bold;
      text-align: left;
      margin-left: 5px;
      margin-top: 5px;
    }

    input {
      border-radius: 5px;
      border: 1px solid #5e5e5e;
      padding-left: 10px;
      height: 30px;
      margin: 5px;
    }
    
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
      -webkit-appearance: none;
    }

    .row {
      display: flex;

      .form__field {
        width: 50%;
        
        &--house {
          max-width: 75px;
        }


        &--index {
          max-width: 100px;
        }

        &--street,
        &--country {
          flex-grow: 1;
        }
      }

    }

    .row--passport {
      flex-wrap: wrap;
      
      &> div {
        flex-grow: 1;
      }
    }

    select {
      margin: 5px;
      min-height: 30px;
      border-radius: 5px;
    }

    .groupClient {
      height: 75px;
      max-width: 150px;

      option {
        margin: 5px;
      }
    }

    small {
        text-align: left;
        margin-left: 5px;
        color: red
    }

    .star {
      color:red;
    }
  }

    .button {
      margin: 10px 50px;
      height: 30px;
      max-width: 250px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
      font-weight: bold;
      color: white;
      background-color: #2c7894;
      text-shadow:0px 1px 0px #262626;
      border: none;
    }

    .modal {
      position: fixed;
      z-index: 100;
      padding-top: 100px;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.4);
      overflow-y: initial
    }
    .modal-content {
      background-color: #fefefe;
      margin: auto;
      padding: 20px;
      border: 1px solid #888;
      width: 80%;
      overflow-y: auto;

      span {
        padding: 5px;
      }
    }

  @media(min-width: 768px) {
    .form {
      width: 700px;
    }

    .modal-content {
      width: 700px
    }
  }
</style>