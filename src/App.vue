<template>
    <div>
        <div>
            <p>
                {{ fromData }} {{ exp }} {{ dataStr }}
            </p>
            <p v-if="nowData != null">
                = {{ nowData }}
            </p>
        </div>
        <table>
            <tr>
                <td>
                    <num-button num=7 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <num-button num=8 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <num-button num=9 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <button v-on:click="divClick">/</button>
                </td>
            </tr>
            <tr>
                <td>
                    <num-button num=4 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <num-button num=5 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <num-button num=6 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <button v-on:click="mulClick">*</button>
                </td>
            </tr>
            <tr>
                <td>
                    <num-button num=1 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <num-button num=2 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <num-button num=3 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <button v-on:click="subClick">-</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button v-on:click="allCancel">C</button>
                </td>
                <td>
                    <num-button num=0 v-on:num-click="numClick"></num-button>
                </td>
                <td>
                    <button v-on:click="numCalculate">=</button>
                </td>
                <td>
                    <button v-on:click="addClick">+</button>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
import NumButton from './components/NumButton.vue'

export default {
    data: function(){
        return{
            dataStr: '',
            nowData: null,
            fromData: null,
            exp: null
        }
    },
    components: {
        'num-button': NumButton
    },
    methods: {
        numClick: function(numClick) {
            if(this.nowData != null)
                this.allCancel();
            this.dataStr += numClick;
        },
        numCalculate: function() {
            if(this.exp == '+')
               this.nowData = this.fromData + parseInt(this.dataStr);
            else if(this.exp == '-')
               this.nowData = this.fromData - parseInt(this.dataStr);
            else if(this.exp == '*')
               this.nowData = this.fromData * parseInt(this.dataStr);
            else if(this.exp == '/')
               this.nowData = this.fromData / parseInt(this.dataStr);
        },
        allCancel: function() {
            this.dataStr = '';
            this.fromData = null;
            this.nowData = null;
            this.exp = null;
        },
        divClick: function() {
            this.numCalculating();
            this.exp = '/';
            this.dataStr = '';
        },
        mulClick: function() {
            this.numCalculating();
            this.exp = '*';
            this.dataStr = '';
        },
        subClick: function() {
            this.numCalculating();
            this.exp = '-';
            this.dataStr = '';
        },
        addClick: function() {
            this.numCalculating();
            this.exp = '+';
            this.dataStr = '';
        },
        numCalculating: function() {
            if(this.nowData == null){
                if(this.dataStr != '')
                   this.fromData = parseInt(this.dataStr); 
            }
            else {
                this.fromData = this.nowData;
                this.nowData = null;
            }
        }
    }
}
</script>

<style>

</style>