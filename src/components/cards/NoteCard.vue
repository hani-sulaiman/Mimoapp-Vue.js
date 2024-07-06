<template>
    <div class="card">
        <div class="head">
            <div class="left">
                <div class="date">{{ formatCreateNoteDate }}</div>
                <div class="title">{{ note.title }}</div>
            </div>
            <div class="right">
                <i class="bi bi-pencil-square"></i>
            </div>
        </div>
        <div class="body">
            <div class="content">
                {{ note.content }}
            </div>
            <div class="reminder">
                <!-- <i class="bi bi-stopwatch"></i>
                <span></span> -->
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        note: Object
    },
    computed: {
        formatCreateNoteDate() {
            const date = new Date(this.note.created_at);
            const year = date.getFullYear();
            const month = date.getMonth() + 1;  // JavaScript months are 0-indexed.
            const day = date.getDate();

            // Pad the month and day with leading zeros if necessary
            const formattedMonth = month < 10 ? `0${month}` : month;
            const formattedDay = day < 10 ? `0${day}` : day;

            return `${year}/${formattedMonth}/${formattedDay}`;
        }
    }
}
</script>