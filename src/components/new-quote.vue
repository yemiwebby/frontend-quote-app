<template>
   <div>
        <div class="col-lg-6 col-md-6 col-sm-6 col-xs-12">
            <form @submit.prevent="onSubmitted">
                <div class="form-group">
                    <label for="content"><b>Quote</b></label><br>
                    <i> Write your quote</i>
                    <br><br>
                    <textarea name="" id="content" class="form-control"  v-model="quoteContent" cols="80" rows="6"></textarea>
                </div>

                <div class="form-group">
                    <button type="submit" class="btn btn-success">
                        Submit
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script type="text/babel">
    import axios from 'axios';
    const baseURL = 'http://localhost:8000/';
    export default {
        data() {
            return {
                quoteContent: ''
            }
        },
        methods: {
            onSubmitted() {
                axios.post(baseURL + '/api/quote',
                        {content: this.quoteContent})
                        .then((response) => {
                        console.log('Quote created!!');
                        window.location.href = "/";
                        })
            .catch ((error) => console.log(error)
            )}
        }
    }
</script>