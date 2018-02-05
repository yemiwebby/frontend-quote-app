<template>
   <div>
        <div class="col-lg-6 col-md-6 col-sm-6 col-xs-12">
            <form @submit.prevent="onSubmitted">
                <div class="form-group">
                    <label for="content">
                        <b>Quote</b>
                        </label>
                        <br>
                    <i> Write your quote here</i>
                    
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
    export default {
        data() {
            return {
                quoteContent: ''
            }
        },
        methods: {
            onSubmitted() {
                axios.post('http://localhost:8000/api/quote',
                        {content: this.quoteContent})
                        .then((res) => {
                        window.location.href = "/";
                        })
            .catch ((err) => console.log(err)
            )}
        }
    }
</script>

<style scoped>
#content {
    margin-top: 40px;
}
</style>
