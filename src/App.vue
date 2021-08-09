<template>
    <div>
        <div>
            <p>
                {{ fromData }} {{ exp }} {{ dataStr }}
            </p>
            <p v-if="nowData != 0">
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
                <!-- <td><one-button v-bind=프롭스 속성이름:"상위컴포넌트 데이터 이름"></one-button></td> -->
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
                    <button v-on:click="oneCancel">◁</button>
                </td>
                <td>
                    <button v-on:click="addClick">+</button>
                </td>
            </tr>
            <tr>
                <td colspan="4">
                    <button v-on:click="numCalculate">
                        =
                    </button>
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
            nowData: 0,
            fromData: 0,
            exp: ''
        }
    },
    components: {
        'num-button': NumButton
    },
    methods: {
        // 현재 numClick이 문자로 인식되는 문제가 있음---------------------------------------------------------
        numClick: function(numClick) {
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
        oneCancel: function() {
        },
        allCancel: function() {
            this.dataStr = '';
            this.fromData = 0;
            this.nowData = 0;
        },
        divClick: function() {
            this.exp = '/';
            this.fromData = parseInt(this.dataStr); 
            this.dataStr = '';
        },
        mulClick: function() {
            this.exp = '*';
            this.fromData = parseInt(this.dataStr);
            this.dataStr = '';
        },
        subClick: function() {
            this.exp = '-';
            this.fromData = parseInt(this.dataStr);
            this.dataStr = '';
        },
        addClick: function() {
            this.exp = '+';
            this.fromData = parseInt(this.dataStr);
            this.dataStr = '';
        }
    }
}
</script>

<style>

</style>