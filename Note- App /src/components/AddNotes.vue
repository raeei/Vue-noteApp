<template>
    <div class="container" style="margin: auto; text-align: center; margin-bottom: 30px;">
        <h3>Add New Notes</h3>
    </div>

    <div class="col-lg-6 col-sm-10 col-sm-8 col-xs-12" style="margin: auto; ">
        <form @submit.prevent="submitAddNotes">
            <base-card>
                <template v-slot:default>
                    <div class="addInput">
                        <label>Title</label>
                        <div>
                            <div class="input-container">
                                <i class="fa fa-pencil icon"></i>
                                <input type="text" v-model.trim="inputTitle" class="input-field"
                                    placeholder="Please add a title....." @blur="validateInputTitle" />
                            </div>

                            <div class="text-right " :class="titleIconContainer">
                                <i class="fa fa-xmark" :class="clearTitle" @click="clearInputTitle"></i>
                            </div>
                            <p :class="errorMegTitle">{{ errorMegTitle1 }}</p>
                        </div>
                        <label>Notes</label>
                        <textarea class="form-control" rows="4" v-model.trim="inputNotes" @blur="validateInputNote"
                            style=""></textarea>
                        <div class="text-right " :class="noteIconContainer">
                            <i class="fa fa-xmark addClear" :class="clearNote" @click="clearInputNote"></i>
                        </div>
                        <p :class="errorMegNote">{{ errorMegNote1 }}</p>
                    </div>
                    <div class="buttons">
                        <base-button type="submit" :class="buttonControl" :disabled="buttonControl ? true : false">Save
                            Note</base-button>
                        <p v-if="error" style="margin-top: 10px;">{{ error }}</p>
                    </div>
                </template>
            </base-card>
        </form>
    </div>

</template>


<script>

export default {
    data() {
        return {
            notes: [],
            inputTitle: '',
            inputNotes: '',
            errorMegNote: 'removeError',
            errorMegNote1: '',
            errorMegTitle: 'removeError',
            errorMegTitle1: '',
            clearTitle: 'removeClearTitle',
            clearNote: 'removeClearNote',
            titleIconContainer: 'editTitleIconContainer',
            noteIconContainer: 'editNoteIconContainer',
            error: null
        }
    },
    watch: {

        // control the input field title's error message as user inputs character
        inputTitle(value) {
            if (value.length > 3) {
                this.errorMegTitle = 'removeError';
            }
            if (value.length > 0) {
                this.clearTitle = 'addClearTitle';
                this.titleIconContainer = 'titleIconContainer'
            } else {
                this.clearTitle = 'removeClearTitle';
                this.titleIconContainer = 'editTitleIconContainer'
            }
        },

        // control the textearea error message as user inputs character
        inputNotes(value) {
            if (value.length > 3) {
                this.errorMegNote = 'removeError';
            } if (value.length > 0) {
                this.clearNote = 'addClearNote';
                this.noteIconContainer = 'noteIconContainer';
            } else {
                this.clearNote = 'removeClearNote';
                this.noteIconContainer = 'editNoteIconContainer';
            }
        },
    },
    computed: {

        // control button availability based on if both input field has more the 3 characters
        buttonControl() {
            if (this.inputTitle.length > 3 && this.inputNotes.length > 3) {
                return null
            } else {
                return 'disabled'
            }
        }
    },
    emits: ['addnew-notes'],
    methods: {

        // validate user's input error messgae based on blur (when focus leaves the input field for title)
        validateInputTitle() {
            if (this.inputTitle === '') {
                this.errorMegTitle = 'addError';
                this.errorMegTitle1 = 'Please this field can be left empty'
            } else if (this.inputTitle.length <= 3) {
                this.errorMegTitle = 'addError';
                this.errorMegTitle1 = 'Please enter 4 or more characters'
            }
            else {
                this.errorMegTitle = 'removeError'
                this.errorMegTitle1 = '';
            }
        },

        // validate user's note error messgae based on blur (when focus leaves the texteara field for note)
        validateInputNote() {
            if (this.inputNotes === '') {
                this.errorMegNote = 'addError';
                this.errorMegNote1 = 'Please this field can be left empty'
            } else if (this.inputNotes.length <= 3) {
                this.errorMegNote = 'addError';
                this.errorMegNote1 = 'Please enter 4 or more characters'
            }
            else {
                this.errorMegNote = 'removeError'
                this.errorMegNote1 = '';
            }
        },

        // the method that clears input field for title when the clear message icon is clicked
        clearInputTitle() {
            this.inputTitle = '';
        },

        // the method that clears textarea field for title when the clear message icon is clicked
        clearInputNote() {
            this.inputNotes = '';
        },

        // the submit button to save new notes (it validates input before emitting an event)
        submitAddNotes() {
            const ranId = new Date().valueOf();
            const start = new Date(2001, 2, 2);
            const end = new Date();
            const randomDate = new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime())).toLocaleDateString();


            if (this.inputTitle === '' || this.inputTitle.length <= 3) {
                this.errorMegTitle = 'addError';
            }
            if (this.inputNotes === '' || this.inputNotes.length <= 3) {
                this.errorMegNote = 'addError'
            }
            else {

                this.error = 'Submitted Successfully';
                        setTimeout(() => {
                            this.error = null;
                            this.$emit('addnew-notes', {
                    id: ranId,
                    title: this.inputTitle,
                    note: this.inputNotes,
                    date: randomDate,
                    changePage: 'saved-notes'
                        });
                         
                        this.inputTitle = '';
                        this.inputNotes = ''
                        }, 1000);
                       

            }
        }
    }
}

</script>

<style scoped>
.addInput {
    padding: 00px 15px 10px 15px;
}

label {
    padding-top: 20px;
}

.buttons {
    padding: 10px 10px 10px 10px;
    margin: auto;
    text-align: center;
}

input {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

textarea {
    padding-right: 35px;
}

input:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.addError {
    display: block;
    color: red;
}

.removeError {
    display: none
}

.disabled {
    color: black;
    background: gray;
    border-color: gray;
    cursor: disabled;
}


.disabled:hover {
    cursor: not-allowed;
    border-color: gray;
    background: gray;
}


.input-container {
    display: flex;
    width: 100%;
}

/* Style the form icons */
.icon {
    padding: 10px;
    background: dodgerblue;
    color: white;
    min-width: 50px;
    text-align: center;
}

/* Style the input fields */
.input-field {
    width: 100%;
    padding: 10px 40px 10px 10px;
    outline: none;
    border-radius: opx;
}

.input-field:focus {
    border: 2px solid dodgerblue;
}

.addClearTitle {
    cursor: pointer;
    display: block;
    font-size: 25px;
    padding: 10px;
}

.removeClearTitle {
    display: none;
    margin-bottom: 70px;
}

.editTitleIconContainer {
    margin-top: 0px;
    margin-bottom: 10px;
}

.titleIconContainer {
    margin-bottom: 11px;
    padding-right: 3px;
    z-index: 2 !important;
    margin-top: -46px;
}

.noteIconContainer {
    margin-bottom: 33px;
    padding-right: 3px;
    z-index: 2 !important;
    margin-top: -75px
}

.editNoteIconContainer {
    margin-top: 0px;
    margin-bottom: 3px;
}

.addClearNote {
    cursor: pointer;
    display: block;
    font-size: 25px;
    padding: 10px;
}

.removeClearNote {
    display: none;
    margin-bottom: 70px;

}
</style>