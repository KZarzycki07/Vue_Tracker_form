<template>
  <div class="background">

<header>
  <h1>Dlaczego nasza firma</h1>
</header>

<div class="contact">
  <h2>Dane Kontaktowe:</h2>
    <ul>
  <li @click="show('777-777-777')" role="button" tabindex="0" @keydown.enter="show('532-235-263')">
Telefon
</li>
<li @click="show('adresmailowy@gmail.com')" role="button" tabindex="0"  @keydown.enter="show('adresmailowy@gmail.com')">
    Email
</li>
<li @click="show('StronaKontaktowa.pl')" role="button" tabindex="0"  @keydown.enter="show('StronaKontaktowa.pl')">
  Strona
</li>
    </ul>
  


   <div class="informacja">
  <p v-if="info">{{ info }}</p>
  </div>
</div>


<main>
<section class="sec1"><h2>O firmie </h2>
<p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Libero deleniti odit laborum alias ducimus. Deleniti voluptate perferendis doloribus perspiciatis! Ab dignissimos voluptatibus aliquid dolor eveniet, quidem sit illum quos porro?</p>
<p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Laudantium porro a cumque neque tempore explicabo eveniet magnam eligendi ab nobis voluptatibus rerum pariatur natus est, exercitationem consequatur earum. Nemo, deleniti.</p>
<p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam nemo dicta recusandae nisi facere incidunt totam. Harum perspiciatis quod rerum nesciunt, voluptatibus repellat ab eum maiores ratione, excepturi fugit natus!</p>
</section>
<section><h2>O nas</h2>
<p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Numquam, illo hic incidunt impedit accusantium reprehenderit animi voluptatem quae dicta. Magnam, asperiores praesentium nesciunt neque sunt voluptatibus accusantium saepe doloribus facere?</p>
<p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Cumque, doloremque, reiciendis dicta ratione expedita quaerat dolorum mollitia, dolor voluptatibus quos fugit asperiores dolore atque aspernatur? Placeat quidem possimus qui? Doloribus!</p>
<p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Ratione, suscipit! Eius soluta, dicta, nihil omnis quas voluptate quasi non veniam error fugiat rem officia molestiae sapiente illo corrupti iste ab?</p>
</section>
</main>

 
  </div>
 


  <footer>
  <h3>Firma XYZ 2026 &copy;</h3>
</footer>
</template>

<script setup lang="ts">
import { ref } from 'vue';





const info = ref<string>("")

function show(value: string) {
  info.value = value
}


</script>

<style lang="scss" scoped>
.background {
 display: flex;
 flex-wrap: wrap;
 background-color: #f6fbfb;
 font-family: 'Montserrat', sans-serif;
}

.contact {
  background-color: #ad96d3;
  width: 100%;
  max-width: 250px;
   min-height: 300px;
  padding: 20px;
  color: #FFFFFF;
  display: flex;
  flex-direction: column;

}

.contact> ul > li{
  display: flex;
  align-items: center;
  margin-top: 30px;
  font-size: 20px;
  padding: 20px;
  transition: 0.3s ease;
  cursor: pointer;

}

.contact > ul > li:hover {
  scale: 110%;
  color: #60A5FA;
}



main {
  flex: 1;
  min-width: 300px;
  width: 100%;
  display: flex;
  align-items: center;
 justify-content: center;

}



header {
  display: flex;
  justify-content: center;
  width: 100%;
  font-size: 24px;
  color: #111827;
}

main > section {

  height: auto;
  background-color: #FFFFFF;
  display: flex;
  border-radius: 20px;
  flex-direction: column;
  border: 1px solid #E5E7EB;
}

main > section > h2 {

  display: flex;
  justify-content: center;
 
}

main > section p {
  color: #4B5563;  
text-align: center;
  font-size: 20px;
  letter-spacing: -0.4px;
}

footer {
  margin-top: 10px;
  display: flex;
  justify-content: end;
  background-color: #111827;
  height: auto;
  padding: 10px;
  color: #FFFFFF;
}

aside {
  
  display: flex;
  flex-direction: column;
}
.contact > .informacja {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  font-size: 17px;
  background-color: #2563EB;
  color: #FFFFFF;
  border-radius: 7px;
}

.informacja {
 margin: auto;
display: flex;
flex-direction: column;
}

.contact > ul > li  {
border: none;
padding: 8px;
font-size: 20px;
outline: none;
color: white;
}


@media(max-width: 768px) {
  .background {
    display: flex;
    flex-direction: column;
  
  }

main {
  flex-direction: column;
    padding: 10px;
}


 .contact {
    max-width: 100%;
    max-height: none;
  }

   main {
    width: 100%;
   }

   section {
   flex: 1;
   margin-top: 5px;
  }


  nav {
    max-width: 100%;
  }

  .informacja {
  margin-top: 20px;
    min-width: 0;
    width: 50% ;
    display: flex;
    justify-content: center;
    position: static;
  }

}

</style>
