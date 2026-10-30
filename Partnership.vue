<template>
  <div class="container">

    <section><h2>HT<span style="color: blue;">ML</span></h2>
        <p>HTML — jest podstawowym językiem używanym do tworzenia stron internetowych i odpowiada za ich strukturę oraz zawartość. Za pomocą HTML tworzy się elementy takie jak nagłówki, akapity, obrazy, linki, formularze, przyciski czy sekcje strony.</p>

        <p>Można powiedzieć, że HTML buduje cały szkielet witryny, który później jest stylowany przez CSS i ożywiany za pomocą JavaScript. Bez HTML strona internetowa nie mogłaby istnieć w swojej podstawowej formie.</p>
    </section>
    <section><h2>C <span style="color: rgb(255, 190, 70);;">SS</span></h2>
       <p>CSS — jest językiem odpowiedzialnym za wygląd oraz układ strony internetowej. Dzięki niemu można zmieniać kolory, czcionki, rozmiary tekstu, odstępy między elementami, dodawać cienie, przejścia i animacje. CSS pozwala również tworzyć nowoczesne oraz responsywne layouty, które dopasowują się do różnych urządzeń</p>
       <p>Za pomocą CSS można stylować praktycznie każdy element strony internetowej i kontrolować jego pozycję, wielkość oraz zachowanie.</p>
    </section>
    <section><h2>Java <span style="color: yellow;">Script</span></h2>
        <p>JavaScript — jest językiem programowania odpowiedzialnym za logikę oraz interaktywność stron internetowych. Dzięki niemu strona może reagować na działania użytkownika, wykonywać animacje, dynamicznie zmieniać treść bez przeładowania oraz komunikować się z serwerami i API.</p>
        <p>JavaScript jest obecnie jednym z najważniejszych języków w web developmencie, ponieważ umożliwia tworzenie nowoczesnych aplikacji internetowych działających płynnie i dynamicznie.</p>
    </section>
    <section><h2>Vue. <span style="color: green;">js</span></h2>
      <p>Vue.js — to nowoczesny framework oparty na JavaScript, wykorzystywany do tworzenia aplikacji internetowych i interfejsów użytkownika. Vue pozwala budować aplikacje z komponentów, co sprawia, że kod jest bardziej uporządkowany, skalowalny i łatwiejszy w utrzymaniu.</p>
      <p>Framework oferuje między innymi reaktywność danych, system routingu, obsługę stanu aplikacji oraz wygodne narzędzia usprawniające pracę frontend developera.</p>
    </section>

  </div>
</template>

<script setup lang="ts">


</script>

<style lang="scss" scoped>
.container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); 
    gap: 24px;
    padding: 40px 20px;
    max-width: 1200px;
    margin: 0 auto; 
    border: none; 
}

section {
    background: #ffffff;
    border: 1.7px solid #eaeaea; 
    border-radius: 16px; 
    padding: 30px;
    transition: all 0.4s ease;


    &:hover {
        transform: translateY(-10px);
        box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1);
        border-color: #3b82f6;
    }

    h2 {
        font-size: 1.4rem;
        margin-bottom: 15px;
        font-weight: 800;
        letter-spacing: -0.5px;
    }
}
</style>