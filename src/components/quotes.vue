<template>
    <div>
        <div class="text-center">
            <button class="btn btn-success" @click="onGetQuotes">
            Get Quotes
             </button>
        </div>
        <hr>

        <app-quote v-for="quote in quotes" :qt="quote" :key="quote.id" @quoteDeleted="onQuoteDeleted($event)"></app-quote>
    </div>
</template>

<script type="text/babel">
    import Quote from './quote.vue';
    import axios from 'axios';

    export default {
        data() {
            return {
                quotes: []
            }
        },
        methods: {
            onGetQuotes() {
                axios.get('http://localhost:8000/api/quotes')
                        .then(
                                response => {
                    this.quotes = response.data.quotes;
                }
                        )
                .catch(
                        error => console.log(error)
                );
            },
            onQuoteDeleted(id) {
                const position = this.quotes.findIndex((element) => {
                            return element.id == id;
                        });
                this.quotes.splice(position, 1);
            }
        },
        mounted: function () {
           this.onGetQuotes();
        },
        components: {
            'app-quote':Quote
        }
    }
</script>