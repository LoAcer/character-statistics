<template>
    <div>
        <el-row>
            <el-col :span="23">
                <div class="block">
                    <span class="demonstration">PRIME1</span>
                    <el-slider v-model="PRIME1" @change="showData"></el-slider>
                </div>
                <div class="block">
                    <span class="demonstration">PRIME2</span>
                    <el-slider v-model="PRIME2" @change="showData"></el-slider>
                </div>
                <div class="block">
                    <span class="demonstration">SLAT</span>
                    <el-slider v-model="SLAT" :max="2234561" :min="1234561" :step="1" @change="showData"></el-slider>
                </div>

                <div class="block">
                    <span class="demonstration">CODE_LENGTH</span>
                    <el-slider v-model="CODE_LENGTH" :max="8" show-stops @change="showData"></el-slider>
                </div>
            </el-col>
        </el-row>

        <line-chart :chart-data="lineChartData" :x-axis="CHARS" />
    </div>
</template>

<script>
import LineChart from "./LineChart";

export default {
    name: "Vode",
    components: {LineChart},
    data() {
        return {
            PRIME1:3,
            PRIME2:11,
            SLAT: 1234561,
            CODE_LENGTH: 6,
            CHARS_LENGTH: 32,
            CHARS:['F', 'L', 'G', 'W', '5', 'X', 'C', '3',
                '9', 'Z', 'M', '6', '7', 'Y', 'R', 'T', '2', 'H', 'S', '8', 'D', 'V', 'E', 'J', '4', 'K',
                'Q', 'P', 'U', 'A', 'N', 'B'],
            val:[],
            lineChartData:  []
        }
    },
    created() {
        this.showData()
    },
    methods:{
        gen(id)
        {
            //补位
            id = id * this.PRIME1 + this.SLAT;
            //将 id 转换成32进制的值
            let b = Array();
            //32进制数
            b[0] = id;
            for (let i = 0; i < this.CODE_LENGTH - 1; i++) {
                b[i + 1] = Math.floor(b[i] / this.CHARS_LENGTH);
                //按位扩散
                b[i] = (b[i] + i * b[0]) % this.CHARS_LENGTH;
            }
            let s = 0;
            for (let j = 0; j < this.CODE_LENGTH - 1; j++) {
                s += b[j];
            }
            b[this.CODE_LENGTH - 1] = s * this.PRIME1 % this.CHARS_LENGTH;


            //进行混淆
            let str = "";
            for (let i = 0; i < this.CODE_LENGTH; i++) {
                //codeIndexArray[i] = b[i * PRIME2 % CODE_LENGTH];
                let index = b[i * this.PRIME2 % this.CODE_LENGTH];
                str = str.concat( this.CHARS[index]);
                this.val[index]++
            }
            // console.log(id, str);
        },
        showData(){
            // console.log(this.PRIME1, this.PRIME2, this.SLAT, this.CODE_LENGTH);
            this.val = [
                0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0
            ];
            for (let i=0;i<100000;i++) {
                this.gen(i);
            }
            this.lineChartData = this.val;
        }
    }
}
</script>

<style scoped>

</style>
