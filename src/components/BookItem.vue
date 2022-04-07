<template>
  <div
    class="container-sm bg-light border border-primary"
        v-bind:class="{
      id: book.id,
      name: book.name,
      price: book.price,
      description: book.description,
      imageUrl: book.imageUrl,
      author: book.author,
      bookCategory: book.bookCategory,
      dateOfRelease: book.dateOfRelease,
    }"
  >
    <div class="row border text-center">
      <div class="col-sm border">
        {{ book.id }}
      </div>
      <div class="col-9">
        {{ book.name }}
      </div>
    </div>

    <div class="row border text-center">
      <div class="col-sm border">
        <img class="img-fluid" v-bind:src="book.imageUrl" />
      </div>
      <div class="col-9 border">
        {{ book.description }}
      </div>
    </div>

    <div class="row border text-center">
      <div class="col-sm border">
        {{ book.price }}
      </div>
      <div class="col-sm border">
        {{ book.author }}
      </div>
      <div class="col-sm border">
        {{ book.bookCategory }}
      </div>
      <div class="col-sm border">
        {{ book.dateOfRelease }}
      </div>
    </div>

    <div class="row border text-center">
      <div class="col-sm border">Cena</div>
      <div class="col-sm border">Autor</div>
      <div class="col-sm border">Typ powieści</div>
      <div class="col-sm border">Rok wydania</div>
    </div>

    <div class="row text-center">
      <div class="col-sm">
        <button class="btn btn-primary" @click="editBook">
          Edytuj książkę
        </button>
      </div>
      <div class="col-sm">
        <button class="btn btn-danger" @click="removeBook">Usuń książkę</button>
      </div>
    </div>
  </div>
  <br />
</template>

<script>
export default {
  name: "bookItem",
  props: ["book"],
  data() {
    return {
      bookId: this.book.id,
    };
  },
  methods: {
    removeBook() {
      this.$emit("removeBookClicked", this.bookId);
    },
    editBook() {
      this.$emit("editBook", this.bookId);
    },
  },
};
</script>
