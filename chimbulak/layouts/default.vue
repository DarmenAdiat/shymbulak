<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="clipped"
      fixed
      stateless
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"
                          style="margin-left: 20px; margin-top: 20px; outline: #dae9f4 auto;border-radius: 10px">
        <v-icon light>mdi-close</v-icon>
      </v-app-bar-nav-icon>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
    >
      <v-app-bar-nav-icon class="post-itm" @click.stop="drawer = !drawer"
                          style="margin-left: 20px; margin-top: 20px; outline: #dae9f4 auto;border-radius: 10px"/>
      <v-app-bar-nav-icon class="post-itm"
                          style="margin-left: 20px; margin-top: 20px; outline: #dae9f4 auto;border-radius: 10px">
        <v-icon light>mdi-magnify</v-icon>
      </v-app-bar-nav-icon>
      <a href="/"><img class='mainlogo' src="/shymbulak-logo.6467f58.svg"
                       style="margin-top: -10px"></a>
      <v-spacer/>
      <v-app-bar-nav-icon style="margin-right: 20px; margin-top: 20px; outline: #dae9f4 auto;border-radius: 10px">
        <v-icon light>mdi-account-outline</v-icon>
      </v-app-bar-nav-icon>
      <v-app-bar-nav-icon style="margin-right: 20px; margin-top: 20px; outline: #dae9f4 auto;border-radius: 10px">
        <v-icon light>mdi-heart-outline</v-icon>
      </v-app-bar-nav-icon>
      <v-app-bar-nav-icon style="margin-right: 20px; margin-top: 20px; outline: #dae9f4 auto;border-radius: 10px">
        <v-icon light>mdi-shopping-outline</v-icon>
      </v-app-bar-nav-icon>
    </v-app-bar>
    <v-container style="margin-top: 60px; max-width: fit-content">
      <v-card-text class="cardtext" style="font-size: xx-large; margin-bottom: 30px; padding-left: 2px">Погода</v-card-text>
      <v-row style="justify-content: center">
        <v-card class="card1"
          outlined
          rounded
          color="#75B6F2">
          <div class="container1">
            <div class="Now">Сейчас</div>
            <div class="Pic">
              <p v-if="todayClo === 'Солнечно'">
                <img class='pic1' src="/sunny.png" style="max-width: 150px; margin-left: 15px">
              </p>
              <p v-if="todayClo === 'Очень солнечно'">
                <img class='pic1' src="/sunny.png" style="max-width: 150px; margin-left: 15px">
              </p>
              <p v-if="todayClo === 'Ясно'">
                <img class='pic1' src="/skycloud.png" style="max-width: 150px; margin-left: 15px">
              </p>
              <p v-if="todayClo === 'Облачно'">
                <img class='pic1' src="/oblachno.png" style="max-width: 150px; margin-left: 15px">
              </p>
            </div>
            <v-row class="Cloud">
              <v-col>
                <div class="clo">{{this.todayClo}}</div>
                <div class="temp">{{this.todayTemp}}°C</div>
                <v-divider style="margin: 0 15px 0 15px"></v-divider>
                <div class="wind">
                  <img class='icons' src="/wind.png">
                  &nbsp;3.64 м.с&nbsp;&nbsp;&nbsp;
                  <img class='icons' src="/drop.png">
                  &nbsp;0.0 см
                </div>
              </v-col>
            </v-row>
          </div>
        </v-card>
        <v-card class="card2"
          outlined
          rounded
          color="#ffffff">
          <div class="container2">
            <div class="DuringDay">Погода в течение дня</div>
            <div class="Divider"><v-divider></v-divider></div>
            <div class="Twelve">
              <v-list style="display: flex; margin: 15px">
                <v-list-item
                  v-for="(item, i) in weather2"
                  :key="i"
                  :to="item.to"
                  exact
                  style="display: block;text-align: center"
                >
                  <v-list-item-title style="-webkit-text-fill-color: #6D7784">
                    {{item.EpochDateTime}}
                  </v-list-item-title>
                  <v-list-item-content>
                    <v-list-item-title>
                      <p v-if="todayClo === 'Солнечно'">
                        <img src="/sunny.png" style="max-width: 35px">
                      </p>
                      <p v-if="todayClo === 'Очень солнечно'">
                        <img src="/sunny.png" style="max-width: 35px">
                      </p>
                      <p v-if="todayClo === 'Ясно'">
                        <img src="/skycloud.png" style="max-width: 35px">
                      </p>
                      <p v-if="todayClo === 'Облачно'">
                        <img src="/oblachno.png" style="max-width: 35px">
                      </p>
                    </v-list-item-title>
                  </v-list-item-content>
                  <v-list-item-content style="padding-top: 5px">
                    <v-list-item-title>{{ Math.ceil((item.Temperature.Value - 32) * 5/9) }}°</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </div>
          </div>
        </v-card>
      </v-row>
      <v-row style="justify-content: center">
      <v-card class="card3"
        outlined
        rounded
        color="#F4F8FD">
        <div class="container3">
          <div class="TenDays">Погода на 10 дней</div>
          <div class="Divider"><v-divider></v-divider></div>
          <div class="TenWeather">
            <v-list class="ThirdBack" style="display: flex">
              <v-list-item
                v-for="(item, i) in ten"
                :key="i"
                :to="item.to"
                exact
                style="display: block; min-width: 121px; max-width: 125px"
              >
                <v-list-item-action>
                  <v-icon>{{ item.day }}</v-icon>
                </v-list-item-action>
                <v-list-item-content>
                  <v-list-item-title><img src="/skycloud.png" style="max-height: 25px"> </v-list-item-title>
                </v-list-item-content>
                <v-list-item-content>
                  <v-list-item-title><a style="-webkit-text-fill-color: dimgray">мин. </a>{{ item.min }}°</v-list-item-title>
                  <v-list-item-title><a style="-webkit-text-fill-color: dimgray">макс. </a>{{ item.max }}°</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </div>
        </div>
      </v-card>
      </v-row>
    </v-container>
    <footer data-v-c73e644a="" data-v-1e103b93="">
      <div data-v-c73e644a="" class="container">
        <div data-v-601faef2="" data-v-c73e644a="" class="info" style="background-color: #212225 !important;">
          <a data-v-601faef2="" href="/ru" aria-current="page"
          class="shymbulak-logo logo nuxt-link-exact-active nuxt-link-active">
          <div data-v-192b4b1a="" data-v-601faef2="">
            <div data-v-192b4b1a="" class="img"><img data-v-192b4b1a="" src="/shymmount.png" alt="">
            </div>
          </div>
          </a>
          <div data-v-601faef2="" class="logo">
            <a data-v-601faef2="" href="/ru" aria-current="page" class="logo nuxt-link-exact-active nuxt-link-active">
            <div data-v-192b4b1a="" data-v-601faef2="">
              <div data-v-192b4b1a="" class="img"><img data-v-192b4b1a="" src="/shymmount.png" alt="">
              </div>
            </div>
            </a>
            <div data-v-601faef2="" class="apps">
              <a data-v-4585199c="" data-v-601faef2="" href="https://play.google.com/store/apps/details?id=kz.shymbulak"
                 target="_blank" class="play-market">
              <div data-v-4585199c="" class="play-market">
                <img data-v-4585199c="" src="/google-play.61ac97c.svg" alt="">
                <div data-v-4585199c="" class="text"><p data-v-4585199c="">Доступно в</p>
                  <h4 data-v-4585199c="">Google Play</h4>
                </div>
              </div>
              </a>
              <a data-v-7972a4f8="" data-v-601faef2=""
                    href="https://apps.apple.com/kz/app/shymbulak-mountain-resort/id1591411405" target="_blank"
                    class="app-store">
              <div data-v-7972a4f8="" class="app-store">
                <img data-v-7972a4f8="" src="/app-store.918d3a6.svg" alt="app-store">
                <div data-v-7972a4f8="" class="text"><p data-v-7972a4f8="">Загрузите в</p>
                  <h4 data-v-7972a4f8="">App Store</h4>
                </div>
              </div>
              </a>
            </div>
          </div>
          <div data-v-621e70f0="" data-v-601faef2="" class="column">
            <h4 data-v-621e70f0="">Курорт</h4>
            <a
            data-v-621e70f0="" href="/ru/hotels" class="">
              <p data-v-621e70f0="">Отели</p>
            </a>
            <a data-v-621e70f0="" href="/ru/restaurants" class="">
              <p data-v-621e70f0="">Рестораны</p>
            </a>
            <a data-v-621e70f0="" href="/ru/entertain" class="">
              <p data-v-621e70f0="">Развлечения</p>
            </a>
            <a data-v-621e70f0="" href="/ru/for-kids" class="">
              <p data-v-621e70f0="">Детям</p>
            </a>
          </div>
          <div data-v-621e70f0="" data-v-601faef2="" class="column">
            <h4 data-v-621e70f0="">Катания</h4>
            <a
            data-v-621e70f0="" href="/ru/tickets" class=""><p data-v-621e70f0="">Билеты</p>
            </a>
            <a data-v-621e70f0=""
                                                                                                  href="/ru/rent"
                                                                                                  class="">
              <p
            data-v-621e70f0="">Прокат</p></a>
            <a data-v-621e70f0="" href="/ru/school" class=""><p data-v-621e70f0="">
            Школа</p></a>
            <a data-v-621e70f0="" href="/ru/parking" class=""><p data-v-621e70f0="">Паркинг</p></a></div>
          <div data-v-621e70f0="" data-v-601faef2="" class="column">
            <h4 data-v-621e70f0="">Инфо</h4>
            <a
            data-v-621e70f0="" href="/ru/weather" class=""><p data-v-621e70f0="">Погода</p></a>
            <a data-v-621e70f0="" href="/ru/info/rules" class="">
              <p data-v-621e70f0="">Правила</p>
            </a>
            <a data-v-621e70f0="" href="/ru/news" class="">
              <p data-v-621e70f0="">Новости</p>
            </a>
            <a data-v-621e70f0="" href="/ru/info/map" class="">
              <p data-v-621e70f0="">Как добраться</p>
            </a>
          </div>
          <div data-v-601faef2="" class="contacts"><h4 data-v-601faef2="">Контакты</h4>
            <div data-v-769e5c16="" data-v-601faef2="" class="socials">
              <a data-v-769e5c16="" href="https://www.instagram.com/shymbulakmountainresort/" target="_blank">
                <img data-v-769e5c16="" src="/instagram.fde2efd.svg" alt="">
              </a>
              <a data-v-769e5c16="" href="https://www.facebook.com/shymbulakmountainresort/" target="_blank">
                <img data-v-769e5c16=""
              src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMzIiIHZpZXdCb3g9IjAgMCAzMiAzMiIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik0wIDVDMCAyLjIzODU4IDIuMjM4NTggMCA1IDBIMjdDMjkuNzYxNCAwIDMyIDIuMjM4NTggMzIgNVYyN0MzMiAyOS43NjE0IDI5Ljc2MTQgMzIgMjcgMzJINUMyLjIzODU4IDMyIDAgMjkuNzYxNCAwIDI3VjVaTTE2IDhDMjAuNCA4IDI0IDExLjYgMjQgMTZDMjQgMjAgMjEuMSAyMy40IDE3LjEgMjRWMTguM0gxOUwxOS40IDE2SDE3LjJWMTQuNUMxNy4yIDEzLjkgMTcuNSAxMy4zIDE4LjUgMTMuM0gxOS41VjExLjNDMTkuNSAxMS4zIDE4LjYgMTEuMSAxNy43IDExLjFDMTUuOSAxMS4xIDE0LjcgMTIuMiAxNC43IDE0LjJWMTZIMTIuN1YxOC4zSDE0LjdWMjMuOUMxMC45IDIzLjMgOCAyMCA4IDE2QzggMTEuNiAxMS42IDggMTYgOFoiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo="
              alt="">
              </a>
              <a data-v-769e5c16="" href="https://api.whatsapp.com/send?phone=77273317777&amp;text=%D0%94%D0%BE%D0%B1%D1%80%D1%8B%D0%B9%20%D0%B4%D0%B5%D0%BD%D1%8C%2C%20%D1%8F%20%D0%BF%D0%BE%20%D0%BF%D0%BE%D0%B2%D0%BE%D0%B4%D1%83..."
                            target="_blank">
                <img data-v-769e5c16="" src="/whatsapp.0aacc07.svg" alt="">
              </a>
              <a data-v-769e5c16="" href="https://vk.com/shymbulakmountainresort" target="_blank">
                <img data-v-769e5c16="" src="/vk.5ab0157.svg" alt="">
              </a>
            </div>
              <p data-v-601faef2=""><a data-v-601faef2="" href="mailto:info@shymbulak.com">info@shymbulak.com</a></p>
              <p data-v-601faef2=""><a data-v-601faef2="" href="tel:+77273317777">+7 727 331 77 77</a></p></div>
        </div>
      </div>
    </footer>
  </v-app>
</template>

<script>
import Vue from 'vue'
import moment from 'moment'
Vue.prototype.$moment = moment;

export default {
  name: 'Shymbulak',
  data() {
    return {
      weather1: [],
      weather2: [
    {
      DateTime: '2023-04-28T12:00:00+06:00',
      EpochDateTime: 11,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 70,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=12',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=12'
    },
    {
      DateTime: '2023-04-28T13:00:00+06:00',
        EpochDateTime: 12,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 71,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=13',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=13'
    },
    {
      DateTime: '2023-04-28T14:00:00+06:00',
        EpochDateTime: 13,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 73,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=14',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=14'
    },
    {
      DateTime: '2023-04-28T15:00:00+06:00',
        EpochDateTime: 14,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 74,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=15',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=15'
    },
    {
      DateTime: '2023-04-28T16:00:00+06:00',
        EpochDateTime: 15,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 73,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=16',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=16'
    },
    {
      DateTime: '2023-04-28T17:00:00+06:00',
        EpochDateTime: 16,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 72,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=17',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=17'
    },
    {
      DateTime: '2023-04-28T18:00:00+06:00',
        EpochDateTime: 17,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 70,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=18',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=18'
    },
    {
      DateTime: '2023-04-28T19:00:00+06:00',
        EpochDateTime: 18,
      WeatherIcon: 1,
      IconPhrase: 'Солнечно',
      HasPrecipitation: false,
      IsDaylight: true,
      Temperature: {
      Value: 68,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=19',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=19'
    },
    {
      DateTime: '2023-04-28T20:00:00+06:00',
        EpochDateTime: 19,
      WeatherIcon: 33,
      IconPhrase: 'Ясно',
      HasPrecipitation: false,
      IsDaylight: false,
      Temperature: {
      Value: 65,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=20',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=20'
    },
    {
      DateTime: '2023-04-28T21:00:00+06:00',
        EpochDateTime: 20,
      WeatherIcon: 33,
      IconPhrase: 'Ясно',
      HasPrecipitation: false,
      IsDaylight: false,
      Temperature: {
      Value: 62,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=21',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=21'
    },
    {
      DateTime: '2023-04-28T22:00:00+06:00',
        EpochDateTime: 21,
      WeatherIcon: 33,
      IconPhrase: 'Ясно',
      HasPrecipitation: false,
      IsDaylight: false,
      Temperature: {
      Value: 59,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=22',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=22'
    },
    {
      DateTime: '2023-04-28T23:00:00+06:00',
        EpochDateTime: 22,
      WeatherIcon: 34,
      IconPhrase: 'Преимущественно ясно',
      HasPrecipitation: false,
      IsDaylight: false,
      Temperature: {
      Value: 58,
        Unit: 'F',
        UnitType: 18
    },
      PrecipitationProbability: 0,
        MobileLink: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=23',
      Link: 'http://www.accuweather.com/ru/kz/chimbulak/65987_poi/hourly-weather-forecast/65987_poi?day=1&hbhhour=23'
    }
  ],
      twelvedata: [],
      clipped: false,
      drawer: false,
      fixed: false,
      todayClo: 'Солнечно',
      todayTemp: '14',
      items: [
        {
          icon: 'mdi-home-outline',
          title: 'Главная',
          to: '/'
        },
        {
          icon: 'mdi-gondola',
          title: 'Билеты',
          to: '/cards'
        },
        {
          icon: 'mdi-safety-goggles',
          title: 'Прокат',
          to: '/b'
        },
        {
          icon: 'mdi-school-outline',
          title: 'Школа',
          to: '/c'
        },
        {
          icon: 'mdi-star-outline',
          title: 'Развлечения',
          to: '/d'
        },
        {
          icon: 'mdi-sofa-single-outline',
          title: 'Отели',
          to: '/e'
        },
        {
          icon: 'mdi-silverware-fork-knife',
          title: 'Рестораны',
          to: '/f'
        },
        {
          icon: 'mdi-store-outline',
          title: 'Магазин',
          to: '/g'
        },
        {
          icon: 'mdi-baby-face-outline',
          title: 'Детям',
          to: '/h'
        },
        {
          icon: 'mdi-parking',
          title: 'Паркинг',
          to: '/j'
        }
      ],
      twelve: [
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
        {
          day: '12',
          cloudiness: 'sun',
          temp: '26'
        },
      ],
      ten: [
        {
          day: 'Сегодня',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Пт',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Сб',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Вс',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Пн',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Вт',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Ср',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Чт',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Пн',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
        {
          day: 'Сб',
          cloudiness: 'Облачно',
          min: '16',
          max: '28'
        },
      ],
      title: 'Vuetify.js'
    }
  },
  created() {
    // this.getWeather()
    // this.getTime()
  },
  methods: {
    async getWeather(){
      this.weather1 = await this.$axios.$get('http://dataservice.accuweather.com/currentconditions/v1/65987_POI?apikey=HtCwRHApvVq3GR9GIGBk6G2EjGVmQst4&language=ru')
      this.weather2 = await this.$axios.$get('http://dataservice.accuweather.com/forecasts/v1/hourly/12hour/65987_POI?apikey=HtCwRHApvVq3GR9GIGBk6G2EjGVmQst4&language=ru')
      console.log(this.weather2)
      this.todayClo = this.weather1[0].WeatherText
      this.todayTemp = this.weather1[0].Temperature.Metric.Value

      for (let i = 0; i<this.weather2.length; i += 1){
        this.weather2[i].EpochDateTime = this.$moment.unix(this.weather2[i].EpochDateTime).format('h')
      }
      // console.log(this.twelvedata)
    },
    // getTime(){
    //   const datet = this.$moment.unix('1682607600').format('h')
    //   console.log(datet)
    // }
  },
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter&family=VT323&display=swap');
.v-application {
  font-family: 'Inter', sans-serif!important;
}
.theme--light.v-app-bar.v-toolbar.v-sheet {
  background-color: #ffffff !important;
  box-shadow: none !important;
}

.theme--light.v-toolbar.v-app-bar.v-app-bar--fixed {
  height: 80px !important;
}

.v-card.v-sheet.v-sheet--outlined.theme--light.rounded {
  border-radius: 17px !important;
}

.container1 {
  display: grid;
  grid-template-columns: 0.4fr 1.6fr;
  grid-template-rows: 0.6fr 1.4fr;
  gap: 0px 0px;
  grid-auto-flow: row;
  grid-template-areas:
    "Now ."
    "Pic Cloud";
}
.container2 {  display: grid;
  grid-template-columns: 0.6fr;
  grid-template-rows: 0.5fr 0.2fr 1.8fr;
  gap: 0px 0px;
  overflow: hidden;
  grid-auto-flow: row;
  grid-template-areas:
    "DuringDay"
    "Divider"
    "Twelve";
}

.container3 {  display: grid;
  grid-template-columns: 0.6fr;
  grid-template-rows: 0.4fr 0.1fr 1.9fr;
  gap: 0px 0px;
  overflow: hidden;
  grid-auto-flow: row;
  grid-template-areas:
    "TenDays"
    "Divider"
    "TenWeather";
}

.TenDays {
  grid-area: TenDays;
  margin: 15px 15px 5px 25px;
  font-weight: 500;
}

.TenWeather { grid-area: TenWeather; }

.Divider {
  grid-area: Divider;
  margin-left: 20px;
  margin-right: 10px;
}

.DuringDay {
  grid-area: DuringDay;
  margin: 15px 15px 5px 25px;
  font-weight: 500;
}

.Twelve {
  grid-area: Twelve;
}

.Now {
  grid-area: Now;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 13px auto auto 20px;
}

.Pic {
  grid-area: Pic;
  align-self: center;
  margin-bottom: 0px!important;
}

.v-application p {
  margin-bottom: 0;
}

.Cloud {
  grid-area: Cloud;
  display: flex;
  align-content: flex-start;
}

.ThirdBack {
  background-color: transparent !important;
  margin: 0 15px 0 15px!important;
}

.v-item-group.v-bottom-navigation .v-btn.v-btn--active {
  color: black;
}

.v-list-item--active {
  background-color: #75B6F2;
  color: white !important;
  border-radius: 12px;
}

.clo {
  margin: 0px 15px 0px 15px;
}

.temp {
  margin-left: 15px;
  font-size: xxx-large;
}

.wind {
  margin: 15px;
  display: flex;
  align-items: center;
}

.card1{
  width: 48.5% !important;
  -webkit-text-fill-color: white!important;
  border-radius: 17px !important;
  margin-right: 5px !important;
  max-height: 220px!important;
}

.card2{
  width:48.5% !important;
  -webkit-text-fill-color: Black !important;
  border-radius: 17px !important;
  margin-left: 5px !important;
  border-color: #dae9f4 !important;
  max-height: 220px!important;
}

.card3{
  -webkit-text-fill-color: black!important;
  border-radius: 17px !important;
  margin-top: 20px!important;
  margin-bottom: 125px!important;
}
.icons{
  max-height: 20px;
}
.theme--light.v-list{
  background-color: transparent!important;
}
footer[data-v-c73e644a] {
  background: #212225 !important;
  color: #fff !important;
  width: 100%!important;
}
footer {
  display: block;
}
.container[data-v-c73e644a] {
  margin-left: auto!important;
  margin-right: auto!important;
  max-width: 1100px!important;
}
.info[data-v-601faef2] {
  display: flex!important;
  flex-wrap: wrap!important;
  padding: 59px 0 54px!important;
  position: relative!important;
}
.info .logo[data-v-601faef2] {
  margin-right: auto!important;
}
.info .stores-info[data-v-601faef2],
.shymbulak-logo[data-v-601faef2] {
   display: none!important;
 }

a[data-v-601faef2] {
   color: #a0a7af!important;
}
.info>div[data-v-601faef2] {
  width: 16.66667%!important;
}
a[data-v-601faef2] {
  color: #a0a7af!important;
}
.img[data-v-192b4b1a] {
  height: 84px!important;
  margin-bottom: 64px!important;
  width: 158px!important;
}
img[data-v-192b4b1a] {
  height: 100%!important;
  width: 100%!important;
}
.app-store[data-v-601faef2], .play-market[data-v-601faef2] {
  border: 1px solid #a6a6a6!important;
  width: 100%!important;
}
 .play-market[data-v-601faef2] {
   margin-bottom: 16px!important;
 }
 .play-market[data-v-4585199c] {
   align-items: center!important;
   border-radius: 15px!important;
   cursor: pointer!important;
   display: flex!important;
   height: 50px!important;
   padding: 8px!important;
 }
.app-store[data-v-601faef2], .play-market[data-v-601faef2] {
  border: 1px solid #a6a6a6!important;
  width: 100%!important;
}
 .app-store[data-v-7972a4f8] {
   align-items: center!important;
   border-radius: 15px!important;
   cursor: pointer!important;
   display: flex!important;
   height: 50px!important;
   padding: 8px!important;
 }
.info>div[data-v-601faef2] {
  width: 16.66667%!important;
}
.info>div h4[data-v-621e70f0] {
  font-size: 21px!important;
  margin-bottom: 24px!important;
}
.info>div p[data-v-621e70f0], a[data-v-621e70f0] {
  color: #a0a7af!important;
  margin-bottom: 16px!important;
}
.info>div h4[data-v-621e70f0] {
  font-size: 21px!important;
  margin-bottom: 24px!important;
}
footer[data-v-c73e644a] {
  background: #212225!important;
  color: #fff!important;
  width: 100%!important;
}
.v-application.info{
  background: #212225!important;
  color: #fff!important;
  width: 100%!important;
}
img[data-v-7972a4f8] {
  filter: invert(100);
  height: 40px;
  width: 40px;
}
img[data-v-4585199c] {
  height: 40px;
  width: 40px;
}
a:link { text-decoration: none!important; }
.socials img[data-v-769e5c16] {
  border-radius: 50%;
  overflow: hidden;
}
.socials[data-v-769e5c16] {
  display: flex;
  gap: 16px;
  margin-bottom: 16px;
}
p[data-v-601faef2] {
  margin-bottom: 16px;
}
.info>div h4[data-v-601faef2] {
  font-size: 21px;
  margin-bottom: 24px;
}
.mainlogo{
  position: fixed;
  top: 50%;
  left: 50%;
}
@media (max-width: 930px) {
  .container[data-v-c73e644a] {
    padding: 0 17px;
  }
}
@media (max-width: 1164px){
  .container[data-v-c73e644a] {

    max-width: 900px;
    padding: 0 17px;
}
  .container[data-v-c73e644a] {
     margin-left: auto;
     margin-right: auto;
     max-width: 1100px;
   }

}
@media (max-width: 1164px) {
  .info > div[data-v-601faef2] {
    width: 25%!important;
  }
}
@media (max-width: 1164px) {
  .apps{
    display: none;
  }
}
@media screen and (max-width: 1500px) {
  .card3{
    width: 75%!important;
  }
  .card1{
    width: 37%!important;
  }
  .card2{
    width: 37%!important;
  }
  .cardtext{
    width: 75%!important;
    margin-left: 150px!important;
  }
}
@media screen and (max-width: 1000px) {
  .pic1{
    max-width: 100px!important;
  }
}
@media screen and (max-width: 850px) {

}

</style>
