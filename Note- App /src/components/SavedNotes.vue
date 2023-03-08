<template>
    <div class="container" style="margin: auto; text-align: center; margin-bottom: 30px;">
        <h3 v-if="notes.length <= 0">Saved notes</h3>
        <h3 v-else>Saved notes  ({{ notes.length }})</h3>
    </div>
    
    <div class="container" style="margin: auto; ">
        <base-card v-if="notes.length <= 0" >
        <template v-slot:default>
            <div class="details text-center">
                <p>No data found, please add notes</p>
            </div>
       </template>
    </base-card>
        <base-card v-else class="basecard" v-for="note in notes" :key="note.id" @click="viewNote(note.id)">
        <template v-slot:default>
            <div class="details">
                <h2>{{ note.title }}</h2>
                <p>{{ note.notes.length > 4 ? note.notes.substr(0, 3) + "..." : note.notes }}</p>
                <h6>Added Date: {{ note.date}}</h6>
            </div>
             
       </template>
    </base-card>  
    </div>
    
</template>

<script>
export default {
inject: [ 'notes', 'viewNote'],
}
</script>


<style scoped>
.details {
    margin-bottom: 10px;
    padding: 20px 15px 20px 15px
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