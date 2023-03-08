<template>
  
  <the-navigation @set-page="setActivePage" ></the-navigation>
  <main>
    <keep-alive>
      <component :is="activePage" @delete-note="deleteNote" @addnew-notes="addNewNote" :id="noteIden" @edit-note="editNote" @update-notes="updateNote" @set-page="setActivePage"></component>
    </keep-alive>
  </main>
 
</template>

<script>
import TheNavigation from './components/Nav/TheNavigation.vue';
import SavedNotes from './components/SavedNotes.vue';
import AddNotes from './components/AddNotes.vue';
import EditNotes from './components/EditNotes.vue';
import ViewNote from './components/ViewNote.vue';

export default {
  components: {
    TheNavigation,
    SavedNotes,
    AddNotes,
    EditNotes,
    ViewNote
  },
  data() {
    return {
      activePage: 'saved-notes',
      notes: [],
      noteIden: ''
      
    }
  },
  methods: {
    // controls the navigation switch
    setActivePage(page) {
      this.activePage = page;
    },

    // to add a new note
    addNewNote(savedNote) {
      const addNewNotes = {
        id: savedNote.id,
        title: savedNote.title,
        notes: savedNote.note,
        date: savedNote.date,
      }
      this.notes.push(addNewNotes);
      this.activePage = savedNote.changePage;
    },

    // to delete a particular note
    deleteNote(noteId){
        const noteIndex = this.notes.findIndex(note => note.id === noteId);
        this.notes.splice(noteIndex, 1);
        this.activePage = 'saved-notes';
      },

      // to view a particular note
      viewNote(note) {     
        this.noteIden = note;
        this.activePage = 'view-note';
      },

      editNote(id){
        this.noteIden = id;
        this.activePage = 'edit-notes';
      },

      // edit a note
      updateNote(updatednote){
        const index = this.notes.findIndex(note => note.id === updatednote.id);
        this.notes[index].title = updatednote.title;
        this.notes[index].notes = updatednote.note;
        this.activePage = updatednote.changePage;

      }
  },
  provide() {
    return {
      notes: this.notes,
      noteIden: this.noteIden,
      viewNote: this.viewNote,
      editNote: this.editNote,
      
    }
  }
}
</script>


<style scoped>
.details {
    border-bottom: 1px solid #eee;
    margin-bottom: 10px;
    padding: 20px 15px 0px 15px
}

.buttons{
    padding: 0px 10px 10px 10px;
    margin: auto;
    text-align: center;
}

.basecard:hover{
    cursor: pointer;
    background: #ddd;
}
</style>
