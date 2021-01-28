<template>
    <div>
<!--        <el-row>-->
<!--            <el-col :span="23">-->
<!--                <div class="block">-->
<!--                    <span class="demonstration">PRIME1</span>-->
<!--                    <el-slider v-model="PRIME1" @change="showData"></el-slider>-->
<!--                </div>-->
<!--            </el-col>-->
<!--        </el-row>-->

        <tree :chart-data="chart" />
    </div>
</template>

<script>
    import Tree from "./Tree";

    export default {
        name: "Node",
        components: {Tree},
        data() {
            return {
                PRIME1:3,
                PRIME2:11,
                val:[],
                chart:  []
            }
        },
        created() {
            this.showData()
            console.log(this.chart)
        },
        methods:{
            gen()
            {

            },
            showData(){
                // console.log(this.PRIME1, this.PRIME2, this.SLAT, this.CODE_LENGTH);
                this.val = [{
                    'name':'fare',
                    'children':[
                        {'name': 'abc', children:[
                                {'name': 'abc-1'},
                                {'name': 'abc-2'},
                                {'name': 'abc-3'},
                            ]
                        },
                        {'name': 'wang', children:[{}]},
                        {'name': '红', children:[{}]},
                    ]
                }]


                this.chart = this.val;
            }
        }
    }
</script>

<style scoped>

</style>
