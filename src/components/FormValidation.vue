<template>
  <form class="form" @submit.prevent="checkForm">
    <h1 class="form__title">Регистрация клиента</h1>
    <div class="info"><u>Основная информация</u></div>
    <div class="form__group">
      <label class="form__label">Фамилия<font color="red">*</font></label>
      <input
        id="lastName"
        type="lastName"
        class="form__input"
        :class="$v.form.lastName.$error ? 'is-invalid' : ''"
        v-model.trim="form.lastName"
      />
      <p
        v-if="$v.form.lastName.$dirty && !$v.form.lastName.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
    </div>
    <div class="form__group">
      <label class="form__label">Имя<font color="red">*</font></label>
      <input
        id="firstName"
        type="firstName"
        class="form__input"
        :class="$v.form.firstName.$error ? 'is-invalid' : ''"
        v-model.trim="form.firstName"
      />
      <p
        v-if="$v.form.firstName.$dirty && !$v.form.firstName.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
      <p
        v-if="$v.form.firstName.$dirty && !$v.form.firstName.minLength"
        class="invalid-feedback"
      >
        Здесь должно быть больше 3-x символов
      </p>
    </div>
    <div class="form__group">
      <label class="form__label">Отчество</label>
      <input
        id="middleName"
        type="middleName"
        class="form__input"
        v-model.trim="form.middleName"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Дата рождения<font color="red">*</font></label>
      <input
        id="dateOfBirth"
        type="date"
        class="form__input"
        :class="$v.form.dateOfBirth.$error ? 'is-invalid' : ''"
        v-model.trim="form.dateOfBirth"
      />
      <p
        v-if="$v.form.dateOfBirth.$dirty && !$v.form.dateOfBirth.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
    </div>
    <div class="form__group">
      <label class="form__label"
        >Номер телефона<font color="red">*</font></label
      >
      <div class="flex">
        <p>+7</p>
        <input
          id="numberPhone"
          type="numberPhone"
          class="form__input"
          :class="$v.form.numberPhone.$error ? 'is-invalid' : ''"
          v-model.trim="form.numberPhone"
        />
      </div>
      <p
        v-if="$v.form.numberPhone.$dirty && !$v.form.numberPhone.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
      <p
        v-if="$v.form.numberPhone.$dirty && !$v.form.numberPhone.minLength"
        class="invalid-feedback"
      >
        Здесь должно быть не меньше 10 символов (без +7)
      </p>
      <p
        v-if="$v.form.numberPhone.$dirty && !$v.form.numberPhone.maxLength"
        class="invalid-feedback"
      >
        Здесь должно быть не больше 10 символов (без +7)
      </p>
      <p
        v-if="$v.form.numberPhone.$dirty && !$v.form.numberPhone.numeric"
        class="invalid-feedback"
      >
        Используйте только цифры
      </p>
    </div>
    <div class="form__group">
      <label class="form__label">Лечащий врач</label>
      <select id="doctor" class="form__input" v-model="form.doctor">
        <option
          v-for="(doctor, index) in doctors"
          :value="doctor.value"
          :key="index"
        >
          {{ doctor.label }}
        </option>
      </select>
    </div>
    <div class="form__group">
      <label class="form__label"
        >Группа клиентов<font color="red">*</font></label
      >
      <select
        id="groupClient"
        class="form__input"
        :class="$v.form.groupClient.$error ? 'is-invalid' : ''"
        v-model.trim="form.groupClient"
        multiple
      >
        <option
          v-for="(groupClient, index) in groupClients"
          :value="groupClient.value"
          :key="index"
        >
          {{ groupClient.label }}
        </option>
      </select>
      <p
        v-if="$v.form.groupClient.$dirty && !$v.form.groupClient.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
    </div>
    <div class="flex">
      <div class="form__group form__check__gender">
        <input
          type="radio"
          class="form__check__input"
          value="male"
          name="exampleRadios"
          id="male"
          v-model="form.gendere"
        />
        <label class="form__check__label" for="male">Мужчина</label>
      </div>
      <div class="form__group form__check__gender">
        <input
          type="radio"
          class="form__check__input"
          value="female"
          name="exampleRadios"
          id="female"
          v-model="form.gendere"
        />
        <label class="form__check__label" for="female">Женщина</label>
      </div>
    </div>
    <div class="form__group form__check">
      <input
        type="checkbox"
        class="form__check__input"
        id="notification"
        v-model="form.agreeWithSendEmail"
      />
      <label class="form__check__label" for="notification"
        >Не отправлять СМС</label
      >
    </div>
    <div class="info"><u>Адрес</u></div>
    <div class="form__group">
      <label class="form__label">Индекс</label>
      <input
        id="index"
        type="index"
        class="form__input"
        v-model.trim="form.index"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Страна</label>
      <input
        id="country"
        type="country"
        class="form__input"
        v-model.trim="form.country"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Область</label>
      <input
        id="region"
        type="region"
        class="form__input"
        v-model.trim="form.region"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Город<font color="red">*</font></label>
      <input
        id="city"
        type="city"
        class="form__input"
        :class="$v.form.city.$error ? 'is-invalid' : ''"
        v-model.trim="form.city"
      />
    </div>
    <p
      v-if="$v.form.city.$dirty && !$v.form.city.required"
      class="invalid-feedback"
    >
      Обязательное поле
    </p>
    <div class="form__group">
      <label class="form__label">Улица</label>
      <input
        id="street"
        type="street"
        class="form__input"
        v-model.trim="form.street"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Дом</label>
      <input
        id="home"
        type="home"
        class="form__input"
        v-model.trim="form.home"
      />
    </div>
    <div class="info"><u>Паспорт</u></div>
    <div class="form__group">
      <label class="form__label">Тип документа<font color="red">*</font></label>
      <select
        id="document"
        class="form__input"
        :class="$v.form.document.$error ? 'is-invalid' : ''"
        v-model="form.document"
      >
        <option
          v-for="(document, index) in documents"
          :value="document.value"
          :key="index"
        >
          {{ document.label }}
        </option>
      </select>
      <p
        v-if="$v.form.document.$dirty && !$v.form.document.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
    </div>
    <div class="form__group">
      <label class="form__label">Серия</label>
      <input
        id="series"
        type="series"
        class="form__input"
        v-model.trim="form.series"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Номер</label>
      <input
        id="number"
        type="numberOfDocument"
        class="form__input"
        v-model.trim="form.number"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Кем выдан</label>
      <input
        id="issued"
        type="issued"
        class="form__input"
        v-model.trim="form.issued"
      />
    </div>
    <div class="form__group">
      <label class="form__label">Дата выдачи<font color="red">*</font></label>
      <input
        id="dateOfIssued"
        type="date"
        class="form__input"
        :class="$v.form.dateOfIssued.$error ? 'is-invalid' : ''"
        v-model.trim="form.dateOfIssued"
      />
      <p
        v-if="$v.form.dateOfIssued.$dirty && !$v.form.dateOfIssued.required"
        class="invalid-feedback"
      >
        Обязательное поле
      </p>
    </div>
    <button class="form__button">Зарегистрироваться</button>
    <p class="necessary">
      <font color="red">*</font>Поле обязательное для заполнения
    </p>
  </form>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  maxValue,
  numeric,
} from "vuelidate/lib/validators";

export default {
  data() {
    return {
      form: {
        lastName: "",
        firstName: "",
        middleName: "",
        dateOfBirth: null,
        numberPhone: null,
        agreeWithSendEmail: false,
        doctor: "",
        groupClient: [],
        gendere: "male",
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        home: "",
        document: "",
        series: "",
        number: "",
        issued: "",
        dateOfIssued: null,
      },
      doctors: [
        {
          label: "Иванов",
          value: "Иванов",
        },
        {
          label: "Захаров",
          value: "Захаров",
        },
        {
          label: "Чернышева",
          value: "Чернышева",
        },
      ],
      groupClients: [
        {
          label: "VIP",
          value: "VIP",
        },
        {
          label: "Проблемные",
          value: "Проблемные",
        },
        {
          label: "ОМС",
          value: "ОМС",
        },
      ],
      documents: [
        {
          label: "Паспорт",
          value: "Паспорт",
        },
        {
          label: "Свидетельство о рождении",
          value: "Свидетельство о рождении",
        },
        {
          label: "Вод. удостоверение",
          value: "Вод. удостоверение",
        },
      ],
    };
  },
  validations: {
    form: {
      lastName: { required, minLength: minLength(5) },
      firstName: { required, minLength: minLength(3) },
      groupClient: { required },
      dateOfBirth: { required },
      numberPhone: {
        required,
        numeric,
        minLength: minLength(10),
        maxLength: maxLength(10),
      },
      city: { required },
      document: { required },
      dateOfIssued: { required },
    },
  },
  methods: {
    checkForm() {
      this.$v.form.$touch();
      if (!this.$v.form.$error) {
        this.submitstatus = alert("Поздравляем! Регистрация прошла успешно!");
        console.log("Данные клиента: ", JSON.stringify(this.$v.form.$model));
      }
    },
  },
};
</script>

<style scoped lang="scss">
.form {
  width: 450px;
  padding: 32px;
  border-radius: 10px;
  box-shadow: 0 2px 20px #ccc;
}

.form__input,
.form__button {
  font-size: 16px;
}

.form__title {
  text-align: center;
  margin: 0 0 32px 0;
  font-weight: normal;
}

.form__group {
  margin-bottom: 25px;
}

.form__label {
  left: 0;
  color: #9e9e9e;
  font-size: 14px;
}

.form__input {
  width: 100%;
  margin-top: 5px;
  padding: 5px 0 5px 0;
  border: none;
  border-bottom: 1px solid #e0e0e0;
  outline: none;
  &:focus {
    border-bottom: 1px solid #1a73a8;
  }
}

.form__button {
  display: block;
  margin: 0 auto;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  color: #fff;
  background-color: #0071f0;
  outline: none;
  cursor: pointer;
  transition: 0.3;
  &:focus {
    background-color: rgba(0, 113, 240, 0.7);
  }
  &:hover {
    background-color: rgba(0, 113, 240, 0.7);
  }
}

.flex {
  display: flex;
  & p {
    margin-right: 2px;
    padding-top: 4px;
  }
}

.form__check__gender {
  margin-right: 10px;
}

.invalid-feedback {
  font-size: 12px;
  color: red;
}

.necessary {
  font-size: 15px;
  margin-top: 35px;
}

.info {
  margin: 15px;
  text-align: center;
}
</style>
