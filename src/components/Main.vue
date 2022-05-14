<template>
  <body>
    <div class="modalWindow" ref="modalWindow" id="777">
      <div class="modalWindow__form">
        <div class="modalWindow__title">Choose a city</div>
        <div class="modalWindow__desk">
          To find city start typing and pick one from the suggestions
        </div>
        <form novalidate>
        <input v-model="inputVal"
          class="modalWindow__input"
          placeholder="in format Paris,FR"
          ref="addCityInput"
          @blur="$v.inputVal.$touch()"
          :class="{'inputError':$v.inputVal.$error}"
          />
        <div v-if="$v.inputVal.$error" class="error">
          Поле обязательно для заполнения
          </div>  
        </form>
        
        
        <div class="modalWindow__buttons">
          <button class="modalWindow__button" @click="clearFormInput">CLEAR</button>
          <div class="modalWindow__add">
            <button class="modalWindow__button"  @click="closeForm">CANCEL</button>
            <button @click="addCity" class="modalWindow__button">ADD</button>
          </div>
        </div>
      </div>
    </div>
    <h1 class="title">World Weather</h1>
    <h2 class="desck">Watch weather in your current location</h2>
    <form class="form">
      <div class="form__title">
        {{ MoscowData.data.name }},{{ MoscowData.data.sys.country }}
      </div>
      <p class="form__desk">Your current location</p>
      <ul class="form__ul">
        <li class="form__li">
          <div>Weather</div>
          <div>{{ MoscowData.data.weather[0].description }}</div>
        </li>
        <li class="form__li">
          <div>Temperature</div>
          <div>{{ Math.round(MoscowData.data.main.temp_max/33.8)}}°</div>
        </li>
        <li class="form__li">
          <div>Humidity</div>
          <div>{{ MoscowData.data.main.humidity }}%</div>
        </li>
        <li>
          <div class="form__time">{{minutesPasses(MoscowData.data.created)}}</div>
        </li>
        <li>
          <button
            class="form__button form__buttonMoscow"
            :id="777"
            :value="MoscowData.data.name"
            @click="reloadItem"
          >
            RELOAD
          </button>
        </li>
      </ul>
    </form>
    <button class="button-add" @click="showModal">ADD CITY</button>
    <div class="form__AddCity">
      <form
        v-for="item in dataCity"
        :key="item.data.id"
        class="form formAddCity"
      >
        <div class="form__title">
          {{ item.data.name }},{{ item.data.sys.country }}
        </div>
        <p class="form__desk">Your current location</p>
        <ul class="form__ul formAddCity__ul">
          <li class="form__li">
            <div>Weather</div>
            <div>{{ item.data.weather[0].description }}</div>
          </li>
          <li class="form__li">
            <div>Temperature</div>
            <div>{{ Math.round(item.data.main.temp_max/33.8) }}°</div>
          </li>
          <li class="form__li">
            <div>Humidity</div>
            <div>{{ item.data.main.humidity }}%</div>
          </li>
          <li>
            <div class="form__time" :id="item.data.id">{{minutesPasses(item.data.created)}}</div>
          </li>
          <li class="form__li formAddCity__li">
            <div class="form__button" :id="item.data.id" @click="removeItem">
              REMOVE
            </div>
            <button
              class="form__button"
              :id="item.data.id"
              :value="item.data.name"
              @click="reloadItem"
            >
              RELOAD
            </button>
          </li>
        </ul>
      </form>
    </div>
    <svg
      class="button__svd-add"
      viewBox="0 0 76 76"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
      @click="showModal"
    >
      <g filter="url(#filter0_ddd_20_7)">
        <path
          d="M10 37C10 21.536 22.536 9 38 9V9C53.464 9 66 21.536 66 37V37C66 52.464 53.464 65 38 65V65C22.536 65 10 52.464 10 37V37Z"
          fill="#9B51E0"
        />
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M45 38H39V44H37V38H31V36H37V30H39V36H45V38Z"
          fill="white"
          fill-opacity="0.87"
        />
      </g>
      <defs>
        <filter
          id="filter0_ddd_20_7"
          x="0"
          y="0"
          width="76"
          height="76"
          filterUnits="userSpaceOnUse"
          color-interpolation-filters="sRGB"
        >
          <feFlood flood-opacity="0" result="BackgroundImageFix" />
          <feColorMatrix
            in="SourceAlpha"
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
            result="hardAlpha"
          />
          <feOffset dy="2" />
          <feGaussianBlur stdDeviation="2" />
          <feColorMatrix
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.2 0"
          />
          <feBlend
            mode="normal"
            in2="BackgroundImageFix"
            result="effect1_dropShadow_20_7"
          />
          <feColorMatrix
            in="SourceAlpha"
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
            result="hardAlpha"
          />
          <feOffset dy="1" />
          <feGaussianBlur stdDeviation="5" />
          <feColorMatrix
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.12 0"
          />
          <feBlend
            mode="normal"
            in2="effect1_dropShadow_20_7"
            result="effect2_dropShadow_20_7"
          />
          <feColorMatrix
            in="SourceAlpha"
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
            result="hardAlpha"
          />
          <feOffset dy="4" />
          <feGaussianBlur stdDeviation="2.5" />
          <feColorMatrix
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.14 0"
          />
          <feBlend
            mode="normal"
            in2="effect2_dropShadow_20_7"
            result="effect3_dropShadow_20_7"
          />
          <feBlend
            mode="normal"
            in="SourceGraphic"
            in2="effect3_dropShadow_20_7"
            result="shape"
          />
        </filter>
      </defs>
    </svg>
  </body>
</template>

<script>
import axios from "axios";
import "@/components/css/style.min.css";
import { required } from 'vuelidate/lib/validators'


export default {
  name: "ProductsList",
  data() {
    return {
      data: [],
      currentCity: "",
      MoscowData: "",
      city: "",
      dataCity: [],
      arrCity: [],
      localCity: [],
      localTimeArr: [],
      tempTimeItem:0,
      inputVal:''
    };
  },
  methods: {
    //показываем модальное окно добавления города
    showModal() {
      this.$refs.modalWindow.style.display = "flex";
    },
    //добавляем город
    addCity() {
      this.city = this.$refs.addCityInput.value;
      localStorage.setItem("city", this.$refs.addCityInput.value);
      this.loadData(this.$refs.addCityInput.value);
      this.$refs.modalWindow.style.display = "none";
    },
    //Делаем запрос API по выбранному городу
    loadData(city) {
      let timeItem = 0;
      axios
        .post(
          "https://api.openweathermap.org/data/2.5/weather?q=" +
            city +
            "+&APPID=769acfb2b423d6376361ff6032d02022"
        )
        .then((response) => {
          // добавим временную метку к созданной карточке
          response.data.created = Date.parse(new Date())
          if (city === "Moscow,RU") {
            this.MoscowData = response;
          } else {
            this.dataCity.push(response);
            localStorage.setItem(
              "arrTimeItem",
              JSON.stringify({
                id: response.data.id,
                time: (timeItem = timeItem + 1),
              })
            );
          }
          this.localTempArr = localStorage.getItem("arrTimeItem");
          this.localTempArr = JSON.parse(this.localTempArr);
          localStorage.setItem("arrCity", JSON.stringify(this.dataCity));
        });
    },
    //удаляем карточку города
    removeItem(event) {
      const findex = (element) => element.data.id == event.target.id;
      let elIndex = this.dataCity.findIndex(findex);
      this.dataCity.splice(elIndex, 1);

      localStorage.setItem("arrCity", JSON.stringify(this.dataCity));
    },
    //обновляем карточку города
    reloadItem(event) {
      const findex = (element) => element.data.id == event.target.id;
      let elIndex = this.dataCity.findIndex(findex);
      this.dataCity.splice(elIndex, 1);
      this.loadData(event.target.value);
    },
    calcTime(event){
       console.log(this.localTempArr);
      return event.target.id
    },
    //вызываем из localStorage cписок городов и делаем API-запрос по каждому 
    loadCity() {
      let localStorageCity = localStorage.getItem("arrCity");
      localStorageCity = JSON.parse(localStorageCity);
      this.localCity = localStorageCity;

      for (let i = 0; i <= this.localCity?.length; i++) {
        this.loadData(this.localCity[i].data.name);
      }
    },

    // отображаем на карточках сколько прошло минут
    minutesPasses(val) {
      const ms = Date.parse(new Date()) - val;
      const min = Math.floor(ms / 60000)
      if (min === 0) {
        return 'Только что'
      }
      if (min % 100 > 4 && min % 100 < 21 || min % 10 === 0) {
        return `Прошло ${min} минут`
      }
      const last_num = min.toString().slice(-1)
      return last_num === '1' ? `Прошла ${min} минута` : ['2','3','4'].includes(last_num) ? `Прошло ${min} минуты ` : `Прошло ${min} минут`

    },
    //очищаем в модальном окне поле ввода "Выбор города" 
    clearFormInput(){
      this.inputVal=''
    },
    //закрываем форму
    closeForm(){
      this.$refs.modalWindow.style.display = "none";
    },

    // запускаем рендер каждую минуту
    reloadEveryMinute(){
      setInterval(()=>{
        console.log('work')
        this.$forceUpdate();
      }, 60000)
    }

  },
  //инициализация валидации поля ввода города
  validations:{
    inputVal:{
      required:required
    }
  },
  //вызываем функции при первой загрузке 
  created() {
    this.loadData("Moscow,RU");
    this.loadCity();
    this.reloadEveryMinute()
    },
};
</script>









