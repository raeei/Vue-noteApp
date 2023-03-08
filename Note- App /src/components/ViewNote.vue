<template>
    <base-dialog v-if="dialogBox" title="Delete Note" @close="confirmError">
    <template #default>
      <p>Are you sure you want to delete  "{{ title }}" note</p>
    </template>
    <template #actions>
      <base-button @click="closeDialogBox" style="margin-right: 10px">Okay</base-button>
      <base-button @click.stop="deleteNote(id)">Delete</base-button>
    </template>
</base-dialog>
      <div class="container" style="margin: auto; text-align: center; margin-bottom: 30px;">
        <h3>Edit notes</h3>
    </div>

    <div class="col-lg-4 col-sm-10 col-sm-8 col-xs-12" style="margin: auto; ">
        <base-card :class="dialogBox ? null : 'basecard'" @click="dialogBox ? null : editNote(id)">
        <template v-slot:default>
            <div class="details">
                <h2>{{ title }}</h2>
                <p>{{ note }}</p>
                <h6>Added Date: {{ date }}</h6>
            </div>
            <div class="buttons">
                <base-button :disabled="dialogBox ? true: false" @click.stop="dialogBox ? null : setActivePage('saved-notes')" style="margin-right: 10px"><i class="fa fa-arrow-left"></i> Go Back</base-button>
                <base-button :disabled="dialogBox ? true: false" @click.stop="openDialogBox">Delete</base-button>
            
            </div>
       </template>
    </base-card>  
    </div>
</template>

<script>
import BaseDialog from './UI/BaseDialog.vue';
export default {
  components: { BaseDialog },
    inject: ['notes', 'editNote'],
    props: ['id'],
    emits: ['set-page', 'delete-Note'],
    data() {
        return{
                dialogBox: false,
                title: '',
                note: '',
                date: ''
        }
    },
    methods: {
        // for the back button
        setActivePage(page) {
            this.$emit('set-page', page);
        },

        // for opening the dialog box
        openDialogBox() {
            this.dialogBox = true;
        },

        // closes the dialog box
        closeDialogBox(){
            this.dialogBox = false
        },

        // emits the id need to delete a particular note.
        deleteNote(id) {
            this.$emit('delete-note', id);
            this.dialogBox = false;

        },

        // To get the particular details for the note once the component is mounted
        loadNote(){
            this.dialogBox = false
            const index = this.notes.findIndex(note => note.id === this.id);
            this.title = this.notes[index].title;
            this.note = this.notes[index].notes;
            this.date = this.notes[index].date;
            
        }
    },

    // triggers a function on mount
    mounted() {
        this.loadNote();
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
    display: flexbox;
}

.basecard:hover{
    cursor: pointer;
    background: #ddd;
}

</style>
