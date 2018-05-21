<template>

    <div class="autocomplete" v-on-clickaway="hide">

        <input type="text" :id="id" :placeholder="placeholder" v-model="query" v-on:keyup="autoComplete" @focus="show = true" class="form-control">

        <div class="autocomplete-items" v-if="results && results.length && show">
            <div v-for="result in results" v-on:click="setSelected(result)">
                    {{ result[search_for] }}
            </div>
        </div>

        <div class="autocomplete-items" v-if="results && !results.length && show">
            <div>
                No results found
            </div>
        </div>

    </div>

</template>

<script>
    import { mixin as clickaway } from 'vue-clickaway';

    export default{
        name: "simple-vue-autocomplete",
        mixins: [ clickaway ],
        props:{
            placeholder: String,
            id: String,
            route: String,
            search_for: String,
            preFill: Object,
            minLength: String
        },
        data(){
            return {
                query: '',
                results: null,
                show : true
            }
        },
        methods: {
            hide(){
                this.show = false
            },
            setSelected(result){
                this.show = false
                this.$emit('selected-result', result)
                this.query = result[this.search_for]
            },
            autoComplete(){
                if(this.query.length >= this.minLength) {

                    this.show = true

                    let data = {
                        "query": {
                            [this.search_for]: this.query
                        }
                    };

                    axios.get(this.route, {params: data}).then(response => {
                        this.results = response.data.data
                    });

                } else {
                    this.hide()
                    this.results = null
                }
            }
        },
        beforeMount(){
            if(this.preFill){
                this.query = this.preFill
            }
        }
    }
</script>



<style scoped>

    .autocomplete {
        position: relative;
    }

    input {
        border: 1px solid transparent;
        padding: 10px;
        font-size: 16px;
    }

    input[type=text] {
        width: 100%;
    }

    input[type=submit] {
        background-color: DodgerBlue;
        color: #fff;
    }

    .autocomplete-items {
        position: absolute;
        border: 1px solid #d4d4d4;
        border-bottom: none;
        border-top: none;
        z-index: 99;
        top: 101%;
        left: 0;
        right: 0;
    }

    .autocomplete-items div {
        padding: 10px;
        cursor: pointer;
        background-color: #fff;
        border-bottom: 1px solid #d4d4d4;
    }

    .autocomplete-items div:hover {
        background-color: #e9e9e9;
    }

    .autocomplete-active {
        background-color: DodgerBlue !important;
        color: #ffffff;
    }

</style>
