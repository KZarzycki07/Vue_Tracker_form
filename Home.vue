<template>
  
  <div :style="{backgroundColor: activeTheme}" class="container" >
<div class="input">
<button class="button" @click="tlo">Kolor</button>
</div>




<input v-model="searchQuery" placeholder="Wyszukaj kryptowalutę" class="search-input">

<select v-model="currency" class="search-value">
  <option value="pln">PLN</option>
  <option value="eur">EUR</option>
  <option value="usd">USD</option>
</select>

<div v-if="!filteredCoins.length">
<p>Brak wyników</p>
</div>

<div v-if="errorinfo">
Błąd pobierania danych <p :style="{color: 'red'}">{{ errorinfo }}</p>
<p>Prosimy zaczekac 30 sekund z ponownym pobraniem</p>
<button @click="coinprice">Pobierz ponownie</button>
</div>

<div v-else-if="loading">
<AppLoader/>
Pobieranie danych
</div>

<div v-else :style="{color: 'green'}" class="success">
  <div v-if="success">
 Pobieranie zakonczone sukcesem!
  </div>
</div>

<div class="grid">

<div v-for="board in filteredCoins" :key="board.id" class="grid2">
<CoinCard :value="board"/>
</div>
</div>


</div>
</template>

<script setup lang="ts">

import {ref ,onMounted, computed,watch,onUnmounted} from 'vue'
import CoinCard from './CoinCard.vue';
import AppLoader from './AppLoader.vue';

export interface Coin {
  id:string,
  name:string,
  current_price: number,
  price_change_percentage_24h: number
    sparkline_in_7d?: {
    price: number[]
  }
}

const activeTheme = ref< 'white' | 'gray' | 'whitesmoke' | 'black'> ('white')


    const coinboard = ref<Coin[]>([]) 

 const searchQuery = ref("")

const debounce = 500

const refreshinterval = 60000

    const currency = ref("pln")

    let delay: ReturnType<typeof setTimeout> | undefined = undefined

    let refresh: ReturnType<typeof setInterval> |undefined = undefined

   const loading = ref<boolean>(true)

    const errorinfo = ref<string | null >(null)

const success = ref<boolean> (false)


let abortController: AbortController | undefined = undefined

    async function coinprice() {
 
     if(abortController) {
     abortController.abort()
     }

     abortController = new AbortController(); //przypisanie wartosci abort(przerywanie zapytan) do zmiennej
     const signal = abortController.signal //przypisanie wartosci nasłuchującej url
 
      errorinfo.value = null // Funkcja startuje więc z początku nie ma błędu

 loading.value = true //Ładowanie danych w toku
      try {

const response = await fetch(`https://api.coingecko.com/api/v3/coins/markets?vs_currency=${currency.value}&order=market_cap_desc&per_page=10&page=1&sparkline=true`, {signal});         

if(!response.ok) {
  throw new Error(`Napotkany błąd: ${response.status}`)
}



const data = await response.json() as Coin[]//Rozpakuj dane

success.value = true //Wyswietl komunikat ze poprawnie pobrano dane,są 100% poprawne jesli nastąpiło juz rozpakowywanie


      coinboard.value = data//Dane ktore zostaly pobrane,przypisz do tablicy
   
    } catch(error) {

    if(error instanceof Error) { //jesli bład pochodzi z rodziny "Error" to mozemy wyciągnąć z niej nazwy lub wiadomość i pokazac uzytkownikowi
      if(error.name === 'AbortError') 
      return
    errorinfo.value = error.message  //przypisujemy oficjalny błąd przewidziany przez przeglądarke
    }

    else {
      errorinfo.value = 'Wystąpił nieznany błąd' // w przeciwym wypadku (else), piszemy ze ten błąd nie jest znany naszej przeglądarce
    }



  success.value = false //Wystąpił blad,wiec ukrywamy success
  }
   
  finally {
    loading.value = false //warunek który ma zostac na samym końcu zawsze wyłączony, bo kręciłby sie bez konca
  }


  }
    onMounted(() => {

      coinprice()


      refresh = setInterval(() => {
        coinprice()
      }, refreshinterval);

       //interwał odswiezania strony co 60 sekund,wpisany do zmiennej refreshinterval
    })



    function tlo() {
      if(activeTheme.value === 'white') {
        activeTheme.value = 'gray'
      }

     else if(activeTheme.value === 'gray') {
        activeTheme.value = 'whitesmoke'
      }
    
      else if (activeTheme.value === 'whitesmoke') {
        activeTheme.value = 'black'
      }
    else {activeTheme.value = 'white'}
    }


watch(searchQuery, () => {
  clearTimeout(delay)
  delay = setTimeout(() => {
    coinprice()
  }, debounce);  
} )
   onUnmounted(()=> {
    clearInterval(refresh)
    clearTimeout(delay)
    //czyszczenie zmiennych by nie działały w tle podczas przełączenia strony
   })


   const filteredCoins = computed(()=> {
  return  coinboard.value.filter(coin => {
   return coin.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    })
   })




</script>

<style lang="scss" scoped>


.container {
  width: 100%;
  min-height: 100vh;
  transition: 0.7s ease;


}

.button {
  background-color: #3b82f6;
  border: none;
  transition: 0.4s ease;
  margin: 15px;
  padding: 5px;
  font-size: 14px;
}

.button:hover {
  background-color: #2579ff;
  scale: 1.1;
}

.grid {
  display: grid;
  justify-content: space-around;
  grid-template-columns: repeat(auto-fit, minmax(200px,1fr));
 grid-template-rows: repeat(2,auto);
 width: 100%;
 margin-top: 3%;
 gap: 40px;
}



.grid2 {
background-color: #ffffff;
padding: 40px;
border-radius: 17px;
transition: 0.4s ease;
border: 1px solid gray;
overflow: hidden;


}

.grid2:hover {
  border: 1px solid blue;
background-color: #ffffff;
scale: 105%;
background-color: #e1e1e1;
}

.search-value {
  margin-left: 10px;
}





@media(max-width: 768px) {
  .theme-slider {
    width: 10%;
  }
}

</style>
