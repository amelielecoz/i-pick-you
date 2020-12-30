<template>
    <div class="row w-100 d-flex align-items-start">
        <div class="col-lg-6 col-md-12 d-flex global-input">
            <div class="w-100 mx-0 d-flex flex-wrap">
                <input 
                    ref="main"
                    class="main-input"
                    type="text"
                    :class="isKeywordEntered? 'd-none' : ''"
                    placeholder="What will you pick?"
                    v-model="input"
                    @input="handleInput"
                >
                <InputItem v-if="isKeywordEntered" :className="'user-name'" :content="inputContent"/>
                <InputItem v-if="isKeywordEntered" :className="'keyword'" :content="keyword"/>
                <InputItem v-if="query !== ''" :className="'pokemon-name'" :content="query"/>
                <input 
                    ref="query"
                    type="text"
                    class="query-input"
                    :class="!isKeywordEntered? 'd-none' : 'd-inline'"
                    v-model="typing"
                    @input="handleQuery"
                    @keydown.delete="handleDelete"
                >
            </div>
            
            
            <div v-if="!input" class="d-flex align-items-center ml-auto">
                <RoutineLogo/>
            </div>
            <div v-if="isItemSelected" class="d-flex align-items-center ml-auto">
                <EnterLogo/>
            </div>
        </div>
        
        <div v-if="isKeywordEntered && itemList.length" class="col-lg-4 col-md-12 d-flex dropdown-list">
            <DropdownList :itemList="itemList" @on-item-selected="selectItem($event)"></DropdownList>
        </div>
    </div>
    
</template>

<script>
import InputItem from './InputItem';
import RoutineLogo from './RoutineLogo';
import EnterLogo from './EnterLogo';
import axios from 'axios';
import DropdownList from './DropdownList.vue';

export default {
    components: {
        InputItem,
        RoutineLogo,
        EnterLogo,
        DropdownList
    },
    data() {
        return {
            isKeywordEntered: false,
            input: '',
            keyword: 'I pick you',
            query: '',
            itemList: [],
            typing: '',
            isItemSelected: false,
        }
    },
    computed: {
        inputContent() {
            return this.input.replace(this.keyword, "");
        }
    },
    created() {
        this.getItemList('');
    },
    mounted() {
        this.$refs.main.focus();
    },
    methods: {
        selectItem(event) {
            this.query = event.phrase;
            this.isItemSelected = true
        },
        handleInput() {
            if(this.input.toLowerCase().includes(this.keyword.toLowerCase())) {
                this.isKeywordEntered = true;
                this.$nextTick(function(){
                    this.$refs.query.focus();
                });
            }
        },
        handleDelete() {
            this.isItemSelected = false;
            // if query is empty
            if(this.isKeywordEntered && (this.query === '')) {
                this.isKeywordEntered = false;
                this.query = '';
                this.$nextTick(function(){
                    this.$refs.main.focus();
                });
            }

            //if query is not empty, we remove last character
            else if (this.isKeywordEntered && (this.query !== '')) {
                this.query = this.query.slice(0, -1);
                this.getItemList(this.query);
            }
        },
        handleQuery() {
            console.log('handleQuery');
            if(this.isKeywordEntered && this.typing !== '') {
                this.query = this.query + this.typing;
                this.typing = '';
            }
            this.getItemList(this.query);
        },
        getItemList(query) {
            axios
                .get(`https://bleeding.routine.co:8080/completion?query=${query}`)
                .then(response => {
                    if (response.status === 200 && response.statusText === 'OK') {
                        this.itemList = response.data.completions;
                    }
                })
                .catch(err => console.log(err));
        }, 
    }
}
</script>
<style>
    .row {
        height: 300px;
        padding-left:24px;
        padding-right:24px;
    }
    
    input {
        background: #F6F3EE;
        border: none;
        color: #444444;
        font-style: normal;
        font-weight: normal;
        font-size: 26px;
        caret-color: #525edd;
        padding: 0;
    }
    .global-input {
        background: #F6F3EE;
        border-radius: 5px;
        padding: 16px 24px !important;
        height: auto;
    }
    .main-input {
        width:100%
    }
    .query-input{
        width: fit-content;
    }
    input:focus {
        outline: none;
    }
    ::placeholder {
        color: #BBB2A1
    }
    .dropdown-list {
        justify-content: start;
    }
</style>