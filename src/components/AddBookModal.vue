<template>
  <div class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <header class="modal-header">
          <div class="container text-center">
            <div class="row">
              <h1>Panel dodawania książki</h1>
            </div>

            <div class="row">
              <h4>Wprowadź dane książki</h4>
            </div>
          </div>
        </header>

        <section class="modal-body">
          <div class="container justify-content-center">
            <div class="row">
              <div class="col-sm"><label for="name">Nazwa:</label></div>
              <div class="col-8">
                <input id="name" type="text" v-model="newName" />
              </div>
            </div>
            <div class="row">
              <div class="col-sm"><label for="price">Cena:</label></div>
              <div class="col-8">
                <input
                  id="price"
                  type="number"
                  min="1"
                  step="0.01"
                  v-model="newPrice"
                />
              </div>
            </div>
            <div class="row">
              <div class="col-sm"><label for="description">Opis:</label></div>
              <div class="col-8">
                <input id="description" type="text" v-model="newDescription" />
              </div>
            </div>
            <div class="row">
              <div class="col-sm"><label for="imageUrl">Zdjęcie:</label></div>
              <div class="col-8">
                <input id="imageUrl" type="text" v-model="newImageUrl" />
              </div>
            </div>
            <div class="row">
              <div class="col-sm"><label for="author">Autor:</label></div>
              <div class="col-8">
                <input id="author" type="text" v-model="newAuthor" />
              </div>
            </div>
            <div class="row">
              <div class="col-sm">
                <label for="bookCategory">Typ powieści:</label>
              </div>
              <div class="col-8">
                <input
                  id="bookCategory"
                  type="text"
                  v-model="newBookCategory"
                />
              </div>
            </div>
            <div class="row">
              <div class="col-sm">
                <label for="dateOfRelease">Rok wydania:</label>
              </div>
              <div class="col-8">
                <input
                  id="dateOfRelease"
                  type="number"
                  min="1800"
                  max="2021"
                  v-model="newDateOfRelease"
                />
              </div>
            </div>
          </div>
        </section>

        <footer class="modal-footer">
          <div class="conatiner">
            <div class="row">
              <div class="col">
                <button class="btn btn-primary" @click="addNewBook()">
                  Dodaj
                </button>
              </div>
              <div class="col">
                <button class="btn btn-danger" @click="closeModal()">
                  Zamknij
                </button>
              </div>
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
