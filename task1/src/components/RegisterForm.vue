<template>
  <div class="form-content" @submit.prevent="submitForm">
    <form autocomplete="off">
      <h3>Личная информация</h3>
      <label for="surname">Фамилия*</label>
      <input id="surname"
             v-model="formData.surname"
             :class="v$.formData.surname.$error ? 'invalid-feedback' : ''"
             required>
      <div v-if="v$.formData.surname.$dirty && v$.formData.surname.$error"
           class="invalid-feedback">Обязательное поле для заполнения!</div>

      <label for="name">Имя*</label>
      <input id="name" v-model="formData.name" required>

      <div v-if="v$.formData.name.$dirty && v$.formData.name.$error"
           class="invalid-feedback">Обязательное поле для заполнения!</div>

      <label for="patronymic">Отчество</label>
      <input id="patronymic" v-model="formData.patronymic">

      <label for="birthdate">Дата рождения*</label>
      <input id="birthdate" type="date" v-model="formData.birthdate" required>

      <div v-if="v$.formData.birthdate.$dirty && v$.formData.birthdate.$error"
           class="invalid-feedback">Обязательное поле для заполнения!</div>

      <label for="phone">Номер телефона*</label>
      <input id="phone" type="tel" v-model="formData.phone" required>

      <div v-if="v$.formData.phone.$dirty && v$.formData.phone.$error"
           class="invalid-feedback">Введите корректный номер!</div>

      <label for="gender">Пол</label>
      <select id="gender" v-model="formData.gender">
        <option value="male">Мужской</option>
        <option value="female">Женский</option>
      </select>

      <label for="customer-group">Группа клиентов*</label>
      <select id="customer-group" v-model="formData.customerGroup" multiple required>
        <option value="VIP">VIP</option>
        <option value="Проблемные">Проблемные</option>
        <option value="ОМС">ОМС</option>
      </select>

      <div v-if="v$.formData.customerGroup.$dirty && v$.formData.customerGroup.$error"
           class="invalid-feedback">Необходимо выбрать группу клиентов!</div>

      <label for="doctor">Лечащий врач</label>
      <select id="doctor" v-model="formData.doctor">
        <option value="Иванов">Иванов</option>
        <option value="Захаров">Захаров</option>
        <option value="Чернышева">Чернышева</option>
      </select>

      <div class="sms-checkbox-container">
        <input id="no-sms" type="checkbox" v-model="formData.noSMS">
        <label for="no-sms" class="no-sms">Не отправлять СМС</label>
      </div>

      <h3>Адрес</h3>
      <label for="index">Индекс</label>
      <input id="index" v-model="formData.address.index">

      <label for="country">Страна</label>
      <input id="country" v-model="formData.address.country">

      <label for="region">Область</label>
      <input id="region" v-model="formData.address.region">

      <label for="city">Город*</label>
      <input id="city" v-model="formData.address.city" required>

      <div v-if="v$.formData.address.city.$dirty && v$.formData.address.city.$error"
           class="invalid-feedback">Обязательное поле для заполнения!</div>

      <label for="street">Улица</label>
      <input id="street" v-model="formData.address.street">

      <label for="house">Дом</label>
      <input id="house" v-model="formData.address.house">

      <h3>Паспортные данные</h3>
      <label for="documentType">Тип документа*</label>
      <select id="documentType" v-model="formData.passport.type" required>
        <option value="Паспорт">Паспорт</option>
        <option value="Свидетельство о рождении">Свидетельство о рождении</option>
        <option value="Вод. удостоверение">Водительское удостоверение</option>
      </select>

      <div v-if="v$.formData.passport.type.$dirty && v$.formData.passport.type.$error"
           class="invalid-feedback">Необходимо указать тип документа!</div>

      <label for="passportSeries">Серия</label>
      <input id="passportSeries" v-model="formData.passport.series">

      <label for="passportNumber">Номер</label>
      <input id="passportNumber" v-model="formData.passport.number">

      <label for="passportIssuedBy">Кем выдан</label>
      <input id="passportIssuedBy" v-model="formData.passport.issuedBy">

      <label for="passportIssueDate">Дата выдачи*</label>
      <input id="passportIssueDate" type="date" v-model="formData.passport.issueDate" required>

      <div v-if="v$.formData.passport.issueDate.$dirty && v$.formData.passport.issueDate.$error"
           class="invalid-feedback">Обязательное поле для заполнения!</div>
    </form>
    <button type="submit" @click="submitForm">Отправить</button>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators';
import useVuelidate from "@vuelidate/core";
export default {
  setup () {
    return { v$: useVuelidate() }
  },
  data() {
    return {
      formData: {
        surname: '',
        name: '',
        patronymic: '',
        birthdate: '',
        phone: '',
        gender: '',
        customerGroup: [],
        doctor: '',
        noSMS: false,
        address: {
          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          house: '',
        },
        passport: {
          type: '',
          series: '',
          number: '',
          issuedBy: '',
          issueDate: ''
        }
      }
    }
  },
  validations: {
    formData: {
      surname: {required},
      name: {required},
      patronymic: {},
      birthdate: {required},
      phone: {
        validatePhoneNumber(phoneNumber) {
          const cleanedPhoneNumber = phoneNumber.replace(/\D/g, '');

          if (cleanedPhoneNumber.length !== 11) {
            return false;
          }

          return /^7\d{10}$/.test(cleanedPhoneNumber);
        }
      },
      gender: {},
      customerGroup: {required},
      doctor: {},
      noSMS: false,
      address: {
        index: {},
        country: {},
        region: {},
        city: {required},
        street: {},
        house: {},
      },
      passport: {
        type: {required},
        series: {},
        number: {},
        issuedBy: {},
        issueDate: {required},
      }
    }
  },
  methods: {
    submitForm() {
      this.v$.formData.$touch();
      if(this.v$.formData.$error) {
        console.log("Форма заполнена некорректно!")
      }
    },
  }
}
</script>

<style scoped>

.form-content {
  display: flex;
  flex-direction: column;
  box-shadow: 0 0 30px #353635; /* Светящаяся тень */
  background: #89948E;
  margin-bottom: 30px;
  padding-top: 20px;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #89948E;
  justify-content: center;
  margin-top: 5px;
}

label {
  font-weight: bold;
}


h3 {
  width: 50%;
  text-align: center;
  border-bottom: 2px solid #2c3e50;
  padding-bottom: 10px;
}

input {
  margin-bottom: 5px;
  width: 300px;
  height: 30px;
  text-align: center;
  align-items: center;
  background: #89948E;
  border: 2px solid #2c3e50;
  outline: none;
  padding: 0;
  color: #353635;
}

input:focus, select:focus {
  border-color: #2c3e50;
  box-shadow: 0 0 5px #353635;
}

select {
  width: 304px;
  background: #89948E;
  border: 2px solid #2c3e50;
  outline: none;
  margin-bottom: 5px;
  color: #353635;
}

#gender, #doctor {
  height: 30px;
}

#customer-group {
  height: 55px;
  outline: none;
}

option {
  text-align: center;
}

.sms-checkbox-container {
  display: flex;
  align-items: center;
}

.no-sms:before {
  background-color: #89948E;
}

#no-sms {
  width: 20px;
  color: #89948E;
  outline: none;
  accent-color: #4A6782;
  background-color: #89948E;
}

#no-sms:focus {
  box-shadow: 0 0 0;
}

#documentType {
  text-align: center;
  height: 35px;
  outline: none;
}

#passportIssueDate {
  margin-bottom: 20px;
}

button {
  color: #cccccc;
  background: #2c3e50;
  border: 1px solid #4A6782;
  padding: 7px 15px;
  border-radius: 3px;
  font-size: 0.9em;
  cursor: pointer;
  margin: 10px 15rem 20px;
}

button:hover {
  background: #4A6782;
}

.invalid-feedback {
  color: #943E3D;
}

</style>