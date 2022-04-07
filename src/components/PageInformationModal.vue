<template>
  <div class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog modal-lg" style="width: 100%" role="document">
      <div class="modal-content">
        <header class="modal-header">
          <div class="container text-center">
            <div class="row">
              <h1>Informacje o stronie</h1>
              <h6>
                Pełna dokumentacja znajduje się w pliku pdf załączonym do
                projektu
              </h6>
            </div>
          </div>
        </header>

        <section class="modal-body">
          <div class="text-justify">
            <b>Autor: Paweł Kalinowski</b>
            <br />
            Poniższy projekt stworzony został na potrzeby przedmiotu
            Architektury i Technologie Systemów Internetowych. Pozwala on na
            zarzadzanie lista książek. Zdecydowano się na aplikacje typu SPA
            (Single Page Application) z powodu zyskującej popularności tego typu
            aplikacji jak również z niskiego progu wejścia dla osób nie
            doświadczonych z front-endem.
            <br />
            <br />
            Wykorzystane technologie:
            <ul>
              <li>Vue.js</li>
              <li>Bootstrap</li>
              <li>Nodej.js, npm</li>
            </ul>
            Wybranym framework’iem front-endowym języka JavaScript w poniższym
            projekcie jest Vue.js. Vue w porównaniu do React lub Angular jest
            znacznie mniej rozbudowany oraz mniej skomplikowany. Sprawia to, że
            łatwiej można w nim tworzyć aplikacje JavaScript, nawet bez
            rozległej wiedzy na temat tego języka. Zaletami Vue są również jego
            mały rozmiar – waży on kilkadziesiąt kilobajtów, a porównaniu do
            innych framework’ów cechuje się tym, iż jest szybszy. Vue posiada
            również dobrą dokumentację projektową. Minusem tego framework’a jest
            brak wsparcia przez wielkie koncerny, przy czym Angular wspierany
            jest przez Google, a React przez Facebooka.
            <br /><br />
            Do layoutu zdecydowano się wykorzystać framework Bootstrap, który
            rozwijany jest przez programistów Twittera oraz dostępny jest na
            licencji MIT. Z tych powodów wykorzystywać go można bezpłatnie,
            nawet w komercyjnych projektach. Dużą zaletą Bootstrap jest szybkość
            tworzenia frontendu stron internetowych. Posiada on wiele gotowych
            komponentów, dlatego tworzenie aplikacji staje się prostsze oraz
            szybsze. Jedną z zalet Bootstrap jest również ułatwienia tworzenia
            stron responsywnych.
            <br /><br />
            W projekcie wykorzystano również Node.js oraz manager pakietów npm,
            które pozwalają na tworzenie aplikacji typu server-side napisanych w
            języku JavaScript.
            <br /><br />
            Poniżej przedstawiono wymagania funkcjonalne aplikacji zrealizowane
            podczas tworzenia projektu:
            <ul>
              <li>możliwość dodawania, edycji oraz usuwania książek z listy</li>
              <li>
                aplikacja działa wyłącznie po stronie przeglądarki (bez części
                serwerowej), co oznacza, że informacje o książkach przechowywane
                są jedynie w pamięci przeglądarki
              </li>
              <li>
                po uruchomieniu aplikacji na liście znajdują się przykładowe 4
                książki
              </li>
              <li>produkty renderowane są za pomocą stworzonego komponentu</li>
              <li>
                lista produktów może zostać posortowana wedle wybranej cechy
              </li>
            </ul>
          </div>
        </section>

        <footer class="modal-footer">
          <div class="conatiner justify-content-center">
            <div class="row">
              <button class="btn btn-danger" @click="closeModal()">
                Zamknij
              </button>
            </div>
          </div>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddBookModal",
  props: ["newBook"],
  data() {
    return {
      newName: "Nowa książka",
      newPrice: 1,
      newDescription: "Nowy opis",
      newImageUrl:
        "https://www.szkolneblogi.pl/static/media/users/private/SPmarzecice/otwarta_ksiazka.jpg",
      newAuthor: "Nowy autor",
      newBookCategory: "Nie zdefiniowano",
      newDateOfRelease: 2016,
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    addNewBook() {
      this.$emit(
        "addNewBook",
        this.newName,
        this.newPrice,
        this.newDescription,
        this.newImageUrl,
        this.newAuthor,
        this.newBookCategory,
        this.newDateOfRelease
      );
    },
  },
};
</script>

<style scoped>
.modal {
  background: #000000c5;
  display: flex;
}
</style>
