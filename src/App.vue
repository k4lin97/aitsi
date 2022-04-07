<template>
  <div class="bg-light" id="app">
    <h1 class="text-center">Lista książek - autor: Paweł Kalinowski</h1>

    <nav class="justify-content-center text-center navbar-light bg-light">
      <div class="container navbar-nav">
        <span class="border border-primary">
          <div class="row nav-item">
            <a class="nav-link" @click="showPageInformationModal()"
              ><b> Informacje o stronie</b></a
            >
          </div>
        </span>

        <br />

        <span>
          <div class="row">
            <div class="col-sm-3">
              <nav
                class="justify-content-center text-center navbar-light bg-light"
              >
                <div class="container navbar-nav">
                  <span class="border border-primary">
                    <div class="row nav-item">
                      <a class="nav-link" @click="showAddBookModal()">
                        <b>Dodaj książkę</b>
                      </a>
                    </div>
                  </span>

                  <br />

                  <span class="border border-primary">
                    <div class="row">
                      <a class="navbar-brand">Sortuj po:</a>
                      <a class="nav-link" @click="sortBooks('all')"
                        >ID książki</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('nameASC')"
                        >Nazwa [rosnąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('nameDESC')"
                        >Nazwa [malejąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('priceASC')"
                        >Cena [rosnąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('priceDESC')"
                        >Cena [malejąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('authorASC')"
                        >Autor [rosnąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('authorDESC')"
                        >Autor [malejąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('bookCategoryASC')"
                        >Typ powieści [rosnąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('bookCategoryDESC')"
                        >Typ powieści [malejąco]</a
                      >
                    </div>
                    <div class="col">
                      <a class="nav-link" @click="sortBooks('dateOfReleaseASC')"
                        >Rok wydania [rosnąco]</a
                      >
                    </div>
                    <div class="col">
                      <a
                        class="nav-link"
                        @click="sortBooks('dateofReleaseDESC')"
                        >Rok wydania [malejąco]</a
                      >
                    </div>
                  </span>

                  <br />

                  <span class="border border-primary">
                    <div class="form-row nav-item">
                      <div class="col-sm">
                        <input
                          class="form-control text-center"
                          name="priceMin"
                          type="number"
                          min="1"
                          placeholder="Cena minimalna"
                          v-model="priceMin"
                        />
                      </div>
                      <div class="col-sm">
                        <input
                          class="form-control text-center"
                          name="priceMax"
                          type="number"
                          min="1"
                          v-model="priceMax"
                          placeholder="Cena maksymalna"
                        />
                      </div>
                    </div>

                    <div class="row nav-item">
                      <div class="col">
                        <a class="nav-link" @click="filterByPrice">
                          Filtruj po cenie
                        </a>
                      </div>
                      <div class="col">
                        <a class="nav-link" @click="resetFilterByPrice">
                          Resetuj filtrowanie
                        </a>
                      </div>
                    </div>
                  </span>
                </div>
              </nav>
            </div>
            <div class="col d-flex justify-content-center">
              <div>
                <BookItem
                  class="book"
                  v-bind:book="book"
                  v-for="book in books"
                  :key="book.id"
                  @removeBookClicked="removeBook"
                  @editBook="showEditBookModal"
                />
              </div>
            </div>
          </div>
        </span>
      </div>
    </nav>
  </div>

  <AddBookModal
    v-show="isAddBookModalVisible"
    @close="closeAddBookModal()"
    @addNewBook="addBook"
  />
  <EditBookModal
    v-show="isEditBookModalVisible"
    @close="closeEditBookModal()"
    @editBookClicked="editBook"
  />
  <PageInformationModal
    v-show="isPageInformationModalVisible"
    @close="closePageInformationModal()"
  />
</template>

<script>
import BookItem from "./components/BookItem.vue";
import AddBookModal from "./components/AddBookModal.vue";
import EditBookModal from "./components/EditBookModal.vue";
import PageInformationModal from "./components/PageInformationModal.vue";

export default {
  name: "App",
  components: {
    BookItem,
    AddBookModal,
    EditBookModal,
    PageInformationModal,
  },
  data() {
    return {
      index: 4,
      books: [
        {
          id: 0,
          name: "Hobbit, czyli tam i z powrotem",
          price: 25.99,
          description:
            "Opowiada o wyprawie podjętej przez krasnoludów tworzących kompanię Thorina i towarzyszącego im hobbita nazwiskiem Bilbo Baggins do zajmowanej przez smoka Smauga Samotnej Góry w celu odzyskania zagarniętych skarbów i dawnej siedziby krasnoludów.",
          imageUrl:
            "https://upload.wikimedia.org/wikipedia/commons/c/c8/HMCoFirstEdSecondPrintTitle.jpg",
          author: "John Ronald Reuel Tolkien",
          bookCategory: "Fantasy",
          dateOfRelease: 1937,
        },
        {
          id: 1,
          name: "Harry Potter i Kamień Filozoficzny",
          price: 44.45,
          description:
            "Powieść jest osadzona w fikcyjnym świecie magii. Jej głównym bohaterem jest jedenastoletni Harry Potter, który dowiaduje się, że jest czarodziejem. Chłopiec rozpoczyna naukę w szkole magii Hogwart, gdzie zaprzyjaźnia się z Ronem Weasleyem i Hermioną Granger.",
          imageUrl:
            "https://image.ceneostatic.pl/data/products/18283/i-harry-potter-i-kamien-filozoficzny.jpg",
          author: "J.K. Rowling",
          bookCategory: "Fantasy",
          dateOfRelease: 1997,
        },
        {
          id: 2,
          name: "Ogniem i mieczem",
          price: 23.99,
          description:
            "Akcja powieści rozgrywa się w latach 1648–1651, w okresie powstania Chmielnickiego na Ukrainie. Pozostałe części Trylogii to Potop i Pan Wołodyjowski. Powieść była pierwotnie wydana w odcinkach w latach 1883–1884 w warszawskim dzienniku „Słowo” i, z minimalnym opóźnieniem w stosunku do „Słowa”, także w krakowskim dzienniku „Czas”.",
          imageUrl:
            "https://upload.wikimedia.org/wikipedia/commons/7/71/Ogniem_I_Mieczem_%281885%29_%28title_page%29.jpg",
          author: "Henryk Sienkiewicz",
          bookCategory: "Powieść historyczna",
          dateOfRelease: 1884,
        },
        {
          id: 3,
          name: "Zbrodnia i kara",
          price: 23.27,
          description:
            "Książka opowiada o perypetiach Rodiona Romanowicza Raskolnikowa, 23-letniego byłego studenta prawa. Rodia był półsierotą, miał jednak kochającą rodzinę. Jego matka Pulcheria Aleksandrowna i siostra Awdotia Romanowna, zwana Dunią, darzyły go głębokim uczuciem, wspierały finansowo i martwiły jego ciężką sytuacją.",
          imageUrl:
            "https://upload.wikimedia.org/wikipedia/commons/c/cd/Cover_of_the_first_edition_of_Crime_and_Punishment.jpg",
          author: "Fiodor Dostojewski",
          bookCategory: "Powieść",
          dateOfRelease: 1867,
        },
      ],
      isAddBookModalVisible: false,
      isEditBookModalVisible: false,
      isPageInformationModalVisible: false,
      bookIdToEdit: -1,
      sortCondition: "all",
      priceMin: null,
      priceMax: null,
      booksWithoutfilter: null,
    };
  },
  methods: {
    showAddBookModal() {
      this.isAddBookModalVisible = true;
    },
    closeAddBookModal() {
      this.isAddBookModalVisible = false;
    },
    showEditBookModal(bookId) {
      this.bookIdToEdit = bookId;
      this.isEditBookModalVisible = true;
    },
    closeEditBookModal() {
      this.isEditBookModalVisible = false;
    },
    showPageInformationModal() {
      this.isPageInformationModalVisible = true;
    },
    closePageInformationModal() {
      this.isPageInformationModalVisible = false;
    },
    addBook(
      newName,
      newPrice,
      newDescription,
      newImageUrl,
      newAuthor,
      newBookCategory,
      newDateOfRelease
    ) {
      this.books.push({
        id: this.index++,
        name: newName,
        price: newPrice,
        description: newDescription,
        imageUrl: newImageUrl,
        author: newAuthor,
        bookCategory: newBookCategory,
        dateOfRelease: newDateOfRelease,
      });
      this.isAddBookModalVisible = false;
    },
    removeBook(bookId) {
      const indextoDelete = this.books.findIndex(
        (element) => element.id === bookId
      );
      this.books.splice(indextoDelete, 1);
    },
    editBook(
      newName,
      newPrice,
      newDescription,
      newImageUrl,
      newAuthor,
      newBookCategory,
      newDateOfRelease
    ) {
      const indexToFind = this.books.findIndex(
        (element) => element.id === this.bookIdToEdit
      );
      this.books[indexToFind].name = newName;
      this.books[indexToFind].price = newPrice;
      this.books[indexToFind].description = newDescription;
      this.books[indexToFind].imageUrl = newImageUrl;
      this.books[indexToFind].author = newAuthor;
      this.books[indexToFind].bookCategory = newBookCategory;
      this.books[indexToFind].dateOfRelease = newDateOfRelease;
      this.isEditBookModalVisible = false;
    },
    sortBooks(event) {
      this.sortCondition = event;
      switch (this.sortCondition) {
        case "all":
          return this.books.sort((a, b) => a.id - b.id);

        case "nameASC":
          return this.books.sort(function (a, b) {
            var upperA = a.name.toUpperCase();
            var upperB = b.name.toUpperCase();
            if (upperA < upperB) {
              return -1;
            }
            if (upperA > upperB) {
              return 1;
            }
            return 0;
          });
        case "nameDESC":
          return this.books.sort(function (a, b) {
            var upperA = a.name.toUpperCase();
            var upperB = b.name.toUpperCase();
            if (upperA > upperB) {
              return -1;
            }
            if (upperA < upperB) {
              return 1;
            }
            return 0;
          });

        case "priceASC":
          return this.books.sort((a, b) => a.price - b.price);
        case "priceDESC":
          return this.books.sort((a, b) => b.price - a.price);

        case "authorASC":
          return this.books.sort(function (a, b) {
            var upperA = a.author.toUpperCase();
            var upperB = b.author.toUpperCase();
            if (upperA < upperB) {
              return -1;
            }
            if (upperA > upperB) {
              return 1;
            }
            return 0;
          });
        case "authorDESC":
          return this.books.sort(function (a, b) {
            var upperA = a.author.toUpperCase();
            var upperB = b.author.toUpperCase();
            if (upperA > upperB) {
              return -1;
            }
            if (upperA < upperB) {
              return 1;
            }
            return 0;
          });

        case "bookCategoryASC":
          return this.books.sort(function (a, b) {
            var upperA = a.bookCategory.toUpperCase();
            var upperB = b.bookCategory.toUpperCase();
            if (upperA < upperB) {
              return -1;
            }
            if (upperA > upperB) {
              return 1;
            }
            return 0;
          });
        case "bookCategoryDESC":
          return this.books.sort(function (a, b) {
            var upperA = a.bookCategory.toUpperCase();
            var upperB = b.bookCategory.toUpperCase();
            if (upperA > upperB) {
              return -1;
            }
            if (upperA < upperB) {
              return 1;
            }
            return 0;
          });

        case "dateOfReleaseASC":
          return this.books.sort((a, b) => a.dateOfRelease - b.dateOfRelease);
        case "dateofReleaseDESC":
          return this.books.sort((a, b) => b.dateOfRelease - a.dateOfRelease);
      }
    },
    filterByPrice() {
      this.booksWithoutfilter = this.books;
      if (this.priceMin && this.priceMax) {
        this.books = this.books
          .filter(
            (book) => book.price >= this.priceMin && book.price <= this.priceMax
          )
          .sort((a, b) => a.price - b.price);
      }
    },
    resetFilterByPrice() {
      if (this.booksWithoutfilter != null) {
        this.books = this.booksWithoutfilter.sort((a, b) => a.id - b.id);
        this.priceMin = null;
        this.priceMax = null;
      }
    },
  },
};
</script>
