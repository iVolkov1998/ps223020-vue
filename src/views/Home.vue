<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-10">
        <h1>Заметки</h1>
        <hr />
        <br /><br />
        <button type="button" class="btn btn-success btn-sm">
          Добавить заметку
        </button>
        <br /><br />
        <table class="table table-hover">
          <thead>
            <tr>
              <th scope="col">Заголовок</th>
              <th scope="col">Заметка</th>
              <th scope="col">Дата создания</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(note, index) in notes" :key="index">
              <td>{{ note.title }}</td>
              <td>{{ note.body }}</td>
              <td>{{ note.createTime }}</td>
              <td>
                <button type="button" class="btn btn-warning btn-sm">
                  Изменить
                </button>
                <button type="button" class="btn btn-danger btn-sm">
                  Удалить
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <b-modal
      ref="addNoteMModal"
      id="book-modal"
      title="Добавим новую заметку"
      hide-footer
    >
      <b-form @submit="onSubmit" @reset="onReset" class="w-100">
        <b-form-group
          id="form-title-group"
          label="Title:"
          label-for="form-title-input"
        >
          <b-form-input
            id="form-title-input"
            type="text"
            v-model="addNoteMForm.title"
            required
            placeholder="Enter title"
          >
          </b-form-input>
        </b-form-group>
        
        <b-form-group
          id="form-author-group"
          label="Author:"
          label-for="form-author-input"
        >
          <b-form-input
            id="form-author-input"
            type="text"
            v-model="addNoteMForm.author"
            required
            placeholder="Enter author"
          >
          </b-form-input>
        </b-form-group>

        <b-form-group id="form-read-group">
          <b-form-checkbox-group v-model="addBookForm.read" id="form-checks">
            <b-form-checkbox value="true">Read?</b-form-checkbox>
          </b-form-checkbox-group>
        </b-form-group>
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </b-form>
    </b-modal>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      notes: [],
      addNoteMForm: {
        title: '',
        body: '',
        createTime: ''
      },
    };
  },
  methods: {
    getNoteMs() {
      const path = "http://localhost:64960/api/NoteMs";
      axios.get(path)
        .then((res) => {
          this.notes = res.data;
        })
        .catch((error) => {
          // eslint-отключение следующей строки
          console.error(error);
        });
    },
    addNoteM(payload) {
      const path = "http://localhost:64960/api/NoteMs";
      axios.post(path, payload)
        .then(() => {
          this.getNoteMs();
        })
        .catch((error) => {
          // eslint-отключение следующей строки
          console.log(error);
          this.getNoteMs();
          console.log("POST запрос был выполнен")
        });
    },
    initForm() {
      this.addNoteMForm.title = '';
      this.addNoteMForm.body = '';
      this.addNoteMForm.createDate = '';
    },
    onSubmit(evt) {
      evt.preventDefault();
      this.$refs.addNoteMModal.hide();
      const payload = {
        title: this.addNoteMForm.Title,
        body: this.addNoteMForm.Body,
        createTime:this.addNoteMForm.CreateDate, // сокращённое свойство
      };
      this.addNoteM(payload);
      this.initForm();
    },
    onReset(evt) {
      evt.preventDefault();
      this.$refs.addNoteMModal.hide();
      this.initForm();
    },
    },
  created() {
    this.getNoteMs();
  },
};
</script>

<style>
</style>