<template>
<div>
    <div v-if="editing">
        <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
            <div class="form-group" id="form__group">
                <label for="content">
                    <b>Edit Quote</b>
                    </label>
                    <br>
                <textarea id="content" v-model="editValue" rows="10" cols="30" class="form-control"></textarea>
                <div class="control_1">
                    <button @click="onUpdate" class="btn btn-success">Save Quote</button>
                    <button @click="onCancel" class="btn btn-danger">Cancel</button>
                </div>
            </div>
        </div>
    </div>
    <div v-if="!editing">
        <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
            <div class="quote-holder">
                <div class="quote">
                    {{ qt.content }}
                </div>

                <div class="quote_control">
                    <div>
                        <div class="control_1">
                            <button @click="onEdit" class="btn btn-primary">
                                Edit
                            </button>
                            <button @click="onDelete" class="btn btn-danger">
                                Delete
                            </button>
                        </div>

                        <div class="control_2">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

</template>

<script type="text/babel">
    import axios from 'axios';

    export default {
        props: ['qt'],
        data() {
            return {
                editing: false,
                editValue: this.qt.content
            }
        },
        methods: {
            onEdit() {
                this.editing = true;
                this.editValue = this.qt.content
            },
            onCancel() {
                this.editing = false;
            },
            onDelete() {
                this.$emit('quoteDeleted', this.qt.id);
                axios.delete('http://localhost:8000/api/quote/' + this.qt.id)
                        .then(
                                res => console.log(res)
            )
            .catch (
                        err => console.log(err)
            )
            },
            onUpdate() {
                this.editing = false;
                this.qt.content = this.editValue;
                axios.put('http://localhost:8000/api/quote/' + this.qt.id,
                        {content: this.editValue})
                        .then(
                                res => console.log(res)
            )
            .catch (
                        err => console.log(err)
            )
                ;
            }
        }
    }
</script>

<style scoped>
    a {
        cursor: pointer;
    }

    .quote {
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    .quote-holder {
        background: #ffffff;
        margin-bottom: 30px;
        position: relative;
        overflow: hidden;
        padding: 20px;
        min-height: 250px;
    }
    .quote_btn {
        border-radius: 0;
        width: 100%;
        display: block;
        cursor: pointer;
    }

    .quote_control {
        width: 100%;
        display: flex;
        padding: 20px 20px 15px;
        background: #FFF;
    }

    .control_1 {
        flex: 2;
    }
    .control_2 {
        flex: 1;
        justify-content: flex-end;
        align-items: center;
        font-size: 20px;
        font-weight: bold;
        color: #51D2B7;
    }

    #form__group{
        box-sizing: border-box;
        overflow: hidden;
    }

    textarea {
        margin: 10px 0;
    }
</style>