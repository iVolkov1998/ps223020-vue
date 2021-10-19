<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-10">
        <h1>Заметки</h1>
        <hr />
        <br /><br />
        <alert :message="message" v-if="showMessage"></alert>
        <button type="button" class="btn btn-success btn-sm" v-b-modal.note-modal>
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
<<<<<<< HEAD
    <b-modal
      ref="addNoteMModal"
      id="book-modal"
      title="Добавим новую заметку"
=======

    <b-modal
      ref="addNoteModal"
      id="note-modal"
      title="Добавьте новую заметку"
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
      hide-footer
    >
      <b-form @submit="onSubmit" @reset="onReset" class="w-100">
        <b-form-group
          id="form-title-group"
<<<<<<< HEAD
          label="Title:"
=======
          label="Заголовок заметки:"
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
          label-for="form-title-input"
        >
          <b-form-input
            id="form-title-input"
            type="text"
<<<<<<< HEAD
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
=======
            v-model="addNoteForm.title"
            required
            placeholder="Введите заголовок"
          >
          </b-form-input>
        </b-form-group>

        <b-form-group
          id="form-body-group"
          label="Текст:"
          label-for="form-body-input"
        >
          <b-form-input
            id="form-body-input"
            type="text"
            v-model="addNoteForm.body"
            required
            placeholder="Введите текст заметки"
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
          >
          </b-form-input>
        </b-form-group>

<<<<<<< HEAD
        <b-form-group id="form-read-group">
          <b-form-checkbox-group v-model="addBookForm.read" id="form-checks">
            <b-form-checkbox value="true">Read?</b-form-checkbox>
          </b-form-checkbox-group>
        </b-form-group>
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
=======
        <b-form-group
          id="form-createTime-group"
          label="Дата создания:"
          label-for="form-createTime-input"
        >
          <b-form-input
            id="form-createTime-input"
            type="text"
            v-model="addNoteForm.createTime"
            required
          >
          </b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Сохранить</b-button>
        <b-button type="reset" variant="danger">Сбросить</b-button>
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
      </b-form>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";
import Alert from "../components/Alert"

export default {
  data() {
    return {
      notes: [],
<<<<<<< HEAD
      addNoteMForm: {
=======
      addNoteForm: {
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
        title: '',
        body: '',
        createTime: ''
      },
<<<<<<< HEAD
=======
      message: '',
      showMessage: false
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
    };
  },
  components: {
    alert: Alert,
  },
  methods: {
<<<<<<< HEAD
    getNoteMs() {
      const path = "http://localhost:64960/api/NoteMs";
      axios.get(path)
=======
    getNotes() {
      const path = "http://localhost:50235/api/Notes";
      axios
        .get(path)
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
        .then((res) => {
          this.notes = res.data;
        })
        .catch((err) => {
          // eslint-отключение следующей строки
          console.error(err);
        });
    },
    addNote(payload) {
      const path = "http://localhost:50235/api/Notes";
      const headers = { 
        "Content-Type": "application/json"
      };
      axios.post(path, payload, { headers })
        .then(() => {
          this.getNotes();
          this.message = "Заметка добавлена";
          this.showMessage = true;
        })
        .catch((error) => {
          // eslint-отключение следующей строки
          console.log(error);
          this.getNotes();
        });
    },
<<<<<<< HEAD
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
=======
    initForm() {
      this.addNoteForm.title = '';
      this.addNoteForm.body = '';
      this.addNoteForm.createTime = '';
    },
    onSubmit(evt) {
      evt.preventDefault();
      this.$refs.addNoteModal.hide();

      const payload = {
        title: this.addNoteForm.title,
        body: this.addNoteForm.body,
        createTime: this.addNoteForm.createTime
      };

      this.addNote(payload);
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
      this.initForm();
    },
    onReset(evt) {
      evt.preventDefault();
<<<<<<< HEAD
      this.$refs.addNoteMModal.hide();
      this.initForm();
    },
    },
=======
      this.$refs.addNoteModal.hide();
      this.initForm();
    },
  },
>>>>>>> 833f4eac43f90408d07d228bf80540879818978e
  created() {
    this.getNoteMs();
  },
};
</script>

<style>
</style>