<template>
    <div class="vue-book">
        <div class="main ivu-article">
            <h1>《Vue.js 实战》预购信息确认</h1>
            <template v-if="order === ''">
                <h2>输入订单号（或手机号）：</h2>
                <Input size="large" v-model="id" placeholder="输入下单时的订单号（或手机号）" style="margin-top: 16px" />
                <Button size="large" type="primary" long style="margin-top: 16px" @click="handleCheck">查询</Button>
            </template>
            <template v-else>
                <h2>订单号 <strong>{{ order.id }}</strong> 信息：</h2>
                <p>
                    <strong>姓名：</strong>
                    <span>{{ order.name }}</span>
                </p>
                <p>
                    <strong>电话：</strong>
                    <span>{{ order.phone }}</span>
                </p>
                <p>
                    <strong>收获地址：</strong>
                    <span>{{ order.address }}</span>
                </p>
                <div style="margin-top: 16px" v-if="isCheck === ''">
                    <Row :gutter="32">
                        <i-col span="12">
                            <Button type="success" size="large" long @click="handleSetCheck(2)">确认无误</Button>
                        </i-col>
                        <i-col span="12">
                            <Button type="warning" size="large" long @click="handleSetCheck(3)">信息有误</Button>
                        </i-col>
                    </Row>
                </div>
                <div style="margin-top: 16px;text-align: center" v-else>
                    <strong>{{ isCheck }}</strong>
                </div>
            </template>
        </div>
    </div>
</template>
<script>

    export default {
        props: {},
        data () {
            return {
                id: '',
                order: '',
                isCheck: ''
            };
        },
        methods: {
            handleCheck () {
                if (this.id === '') {
                    this.$Notice.error({
                        title: '请输入订单号'
                    });
                } else {
                    const params = new URLSearchParams();
                    params.append('id', this.id);

                }
            },
            handleSetCheck (type) {
                const params = new URLSearchParams();
                params.append('id', this.order.id);
                params.append('check', type);

            }
        },
        mounted () {
            document.body.style.background = '#f8f8f9';
            document.body.style.height = '100%';
            document.getElementsByTagName('html')[0].style.height = '100%';
            document.getElementsByTagName('div')[0].style.height = '100%';
        }
    };
</script>
<style scoped>
    .vue-book{
        width: 60%;
        min-height: 100%;
        margin: 0 auto;
        padding: 16px;
        background: #fff;
        box-shadow: 0 2px 2px rgba(0,0,0,.2);
    }
    h1{
        text-align: center;
    }
    .steps{
        margin: 16px 0 32px;
    }
    .order{
        padding: 16px;
    }
</style>