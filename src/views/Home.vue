<template>
    <div class="home">
        <div class="container">
            <div class="panel" v-bind:style="`transform: scale(${scale / 100}) translate(${offsetX}px, ${offsetY}px);`">
                <div class="header">
                    <div class="row" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                        <h4 class="title">胜博物流</h4>
                        <h4 class="title">内蒙古专线</h4>
                        <span class="subTitle">货物托运单</span>
                    </div>
                    <div class="options">
                        <div class="item">
                            <span class="itemTitle" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">日期：</span>
                            <div class="itemContent">
                                <el-date-picker class="datePicker" v-model="date" type="date"></el-date-picker>
                                <div class="showDate">
                                    <div class="number year">{{date ? date.getFullYear() : ''}}</div>
                                    <div class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">年</div>
                                    <div class="number date">{{date ? date.getMonth() + 1 : ''}}</div>
                                    <div class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">月</div>
                                    <div class="number date">{{date ? date.getDate() : ''}}</div>
                                    <div class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">日</div>
                                </div>
                            </div>
                        </div>
                        <div class="item">
                            <span class="itemTitle" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">直达</span>
                            <div class="itemContent">
                                <input v-model="directAccess"/>
                            </div>
                        </div>
                        <div class="item">
                            <span class="itemTitle" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">中转</span>
                            <div class="itemContent">
                                <input v-model="transfer"/>
                            </div>
                        </div>
                        <div class="item">
                            <span class="itemTitle" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">YM：</span>
                            <div class="itemContent" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                                <input v-model="ym"/>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="body">
                    <div class="row">
                        <div class="col">
                            <div class="row">
                                <div class="col" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                                    <h4>
                                        <p>收货单位/人</p>
                                        <p>(收货代号)</p>
                                    </h4>
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input v-model="name"/>
                                </div>
                                <div class="col" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                                    <div>电话</div>
                                    <div>地址</div>
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <div class="phone" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                        <input v-model="phone"/>
                                    </div>
                                    <div class="address">
                                        <input v-model="address"/>
                                    </div>
                                </div>
                            </div>
                            <div class="row" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                                <div class="col greyBg">货物名称</div>
                                <div class="col greyBg">包装样式</div>
                                <div class="col greyBg">件数</div>
                                <div class="col greyBg" style="letter-spacing: -2px;">重量(体积)</div>
                                <div class="col greyBg">外付款</div>
                                <div class="col greyBg">内收款</div>
                                <div class="col greyBg">内欠款</div>
                            </div>
                            <div class="row">
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <div class="col packing" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <el-select v-model="packing" placeholder="">
                                        <el-option v-for="(item) in packingOptions" :key="item" :label="item" :value="item"></el-option>
                                    </el-select>
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <!-- <div class="col" v-on:click="value1 = '1'"> -->
                                <div class="col" v-on:click="setCheck('value1', '1')" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <i v-if="value1 == '1'" class="el-icon-check"></i>
                                </div>
                                <div class="col" v-on:click="setCheck('value1', '2')" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <i v-if="value1 == '2'" class="el-icon-check"></i>
                                </div>
                                <div class="col" v-on:click="setCheck('value1', '3')" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <i v-if="value1 == '3'" class="el-icon-check"></i>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <div class="col" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <input />
                                </div>
                                <div class="col" v-on:click="setCheck('value2', '1')" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <i v-if="value2 == '1'" class="el-icon-check"></i>
                                </div>
                                <div class="col" v-on:click="setCheck('value2', '2')" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <i v-if="value2 == '2'" class="el-icon-check"></i>
                                </div>
                                <div class="col" v-on:click="setCheck('value2', '3')" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <i v-if="value2 == '3'" class="el-icon-check"></i>
                                </div>
                            </div>
                            <div class="row" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                <div class="amount" v-bind:style="`background-color: ${mode == 'input' ? 'rgb(220, 220, 220)' : 'transparent'};`">
                                    <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">合计：</span>
                                    <input />
                                </div>
                                <div class="cost">
                                    <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">直送费：</span>
                                    <input style="text-align: center;"/>
                                    <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">元</span>
                                </div>
                            </div>
                            <div class="row" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                <div class="totalTitle" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                    <div v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                                        <h4>合计金额</h4>
                                        <span>(大写)</span>
                                    </div>
                                </div>
                                <div class="totalContent">
                                    <div class="item capitalizedNumber">
                                        <el-select placeholder="" v-model="amountList[0]" v-on:change="computeMoney">
                                            <el-option v-for="(item, index) in numberOptions" :key="index" :label="item.label" :value="item.value"></el-option>
                                        </el-select>
                                        <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">万</span>
                                    </div>
                                    <div class="item capitalizedNumber">
                                        <el-select placeholder="" v-model="amountList[1]" v-on:change="computeMoney">
                                            <el-option v-for="(item, index) in numberOptions" :key="index" :label="item.label" :value="item.value"></el-option>
                                        </el-select>
                                        <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">仟</span>
                                    </div>
                                    <div class="item capitalizedNumber">
                                        <el-select placeholder="" v-model="amountList[2]" v-on:change="computeMoney">
                                            <el-option v-for="(item, index) in numberOptions" :key="index" :label="item.label" :value="item.value"></el-option>
                                        </el-select>
                                        <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">佰</span>
                                    </div>
                                    <div class="item capitalizedNumber">
                                        <el-select placeholder="" v-model="amountList[3]" v-on:change="computeMoney">
                                            <el-option v-for="(item, index) in numberOptions" :key="index" :label="item.label" :value="item.value"></el-option>
                                        </el-select>
                                        <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">拾</span>
                                    </div>
                                    <div class="item capitalizedNumber">
                                        <el-select placeholder="" v-model="amountList[4]" v-on:change="computeMoney">
                                            <el-option v-for="(item, index) in numberOptions" :key="index" :label="item.label" :value="item.value"></el-option>
                                        </el-select>
                                        <span class="text" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">元</span>
                                    </div>
                                    <div class="number">
                                        <i v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">¥：</i>
                                        <input ref="money" v-model="money" type="number" v-on:input="inputMoney" v-on:blur="blurFunc" v-on:keydown="keydownFunc"/>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col">
                            <div class="markTitle greyBg" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">备注</div>
                            <textarea class="mark" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`"></textarea>
                            <div class="row" v-bind:style="`border-color: ${mode == 'input' ? 'black' : 'transparent'};`">
                                <span class="personalTitle greyBg" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">开票人</span>
                                <input >
                            </div>
                        </div>
                    </div>
                    <div class="otherInfo" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                        <div class="item">
                            <span class="title">运输</span>
                            <span class="content">(1)发货人必须持有效证件；不准携带夹带国家违禁物品、瞒报危险物品及自觉检查货物；配合工作人员开箱检查货物工作。</span>
                        </div>
                        <div class="item">
                            <span class="title">运货</span>
                            <span class="content">(2)发货人应认真核对上述各项数据，若有差错，后果自负；并按有关法规办理托运事宜。凭本单据限30天核对查询有效。</span>
                        </div>
                        <div class="item">
                            <span class="title">须知</span>
                            <span class="content">(3)托运物品，自愿参加货物保险，并声明实际价值；如若货物未保险而发生货损货失等意外，最高赔偿金额不超过运费的10倍；</span>
                        </div>
                    </div>
                </div>
                <div class="footer" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
                    <div class="row">
                        <div class="item">
                            <span>物流地址：</span>
                            <span>乐清市柳市镇环城北路181号（德力西高科园）</span>
                        </div>
                        <div class="item">
                            <span>包头提货：</span>
                            <span>15847276363</span>
                        </div>
                    </div>
                    <div class="row">
                        <div class="item">
                            <span>物流电话：</span>
                            <span>0577-62781825</span>
                        </div>
                        <div class="item">
                            <span>手机：</span>
                            <span>13868789986</span>
                        </div>
                        <div class="item">
                            <span>呼市提货：</span>
                            <span>15184700039</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="testBox" style="position: fixed; left: -144px; top: -140px; opacity: 0.5; pointer-events: none;" v-show="state">
            <img v-bind:src="img"/>
        </div>
        <div class="control" v-bind:style="`opacity: ${mode == 'input' ? 1 : 0};`">
            <div class="item">
                <span class="itemTitle">左右位置</span>
                <div class="itemContent">
                    <el-slider v-bind:step="1" v-model="offsetX" v-bind:min="-500" v-bind:max="500"></el-slider>
                    <input size="mini" v-model="offsetX" />
                </div>
            </div>
            <div class="item">
                <span class="itemTitle">上下位置</span>
                <div class="itemContent">
                    <el-slider v-bind:step="1" v-model="offsetY" v-bind:min="-500" v-bind:max="500"></el-slider>
                    <input size="mini" v-model="offsetY" />
                </div>
            </div>
            <div class="item">
                <span class="itemTitle">放大比例</span>
                <div class="itemContent">
                    <el-slider v-bind:step="1" v-model="scale" v-bind:min="10" v-bind:max="500"></el-slider>
                    <input size="mini" v-model="scale" />
                </div>
            </div>
            <el-button style="margin-left: 50px;" type="primary" v-on:click="printPage" size="small">打印</el-button>
            <!-- <el-button type="primary" v-on:click="testFunc" size="small">对比</el-button> -->
        </div>
    </div>
</template>
<script>
// import img from '../assets/bg.png'
export default {
    components: {},
    data: function () {
        return {
            // img,
            date: '',
            directAccess: '',
            transfer: '',
            ym: '888888',
            name: '',
            phone: '',
            address: '',
            value1: '0',
            value2: '0',
            mode: 'input',
            // mode: 'print',
            packingOptions: ['纸箱', '木箱', '袋子', '木架', '起动柜', '柜子', '变压器'],
            packing: '',
            // numberOptions: ['壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'],
            numberOptions: [{
                value: 1,
                label: '壹'
            }, {
                value: 2,
                label: '贰'
            }, {
                value: 3,
                label: '叁'
            }, {
                value: 4,
                label: '肆'
            }, {
                value: 5,
                label: '伍'
            }, {
                value: 6,
                label: '陆'
            }, {
                value: 7,
                label: '柒'
            }, {
                value: 8,
                label: '捌'
            }, {
                value: 9,
                label: '玖'
            }],
            amountList: ['', '', '', '', ''],
            scale: 100,
            money: '',
            state: 0,
            offsetX: 0,
            offsetY: 0
        }
    },
    methods: {
        setCheck: function (key, val) {
            (this[key] === val) ? (this[key] = '0') : (this[key] = val)
        },
        printPage: function () {
            this.mode = 'print'
            this.$nextTick(() => {
                window.print()
            })
        },
        computeMoney: function () {
            let sum = 0
            this.amountList.forEach((item, index) => {
                sum = sum + item * Math.pow(10, (4 - index))
            })
            this.money = sum + '.00'
        },
        inputMoney: function () {
            /* eslint-disable */
            let arr = parseInt(this.money).toString().match(/\d/g)
            while (arr.length < 5) {
                arr.unshift('')
            }
            arr.forEach((item, index) => {
                this.amountList[index] = parseInt(item) || ''
            })
        },
        blurFunc: function () {
            let number = Number(this.money) || 0
            this.money = number.toFixed(2)
        },
        keydownFunc: function (event) {
            if (event.keyCode === 13) {
                this.blurFunc()
                this.$refs.money.blur()
            }
        },
        testFunc: function () {
            this.state = (this.state + 1) % 2
        }
    },
    mounted: function () {
        window.onbeforeprint = () => {
            this.mode = 'print'
        }
        window.onafterprint = () => {
            this.mode = 'input'
        }
    }
}

</script>
<style lang="stylus" scoped>
    blackColor = #000
    .home {
        .greyBg {
            background-color: rgb(220, 220, 220);
            -webkit-print-color-adjust: exact;
        }
        input {
            background-color: transparent;
        }
        .container {
            margin-top: 10px;
            margin-left: 10px;
            .panel {
                // width: 1143px;
                width: 810px;
                height: 692px;
                transform-origin: top left;
                // background-image: url('~@/assets/bg.png');
            }
            .header {
                padding-top: 23px;
                .row {
                    font-size: 0;
                    padding-left: 52px;
                    .title {
                        font-size: 43px;
                        display: inline-block;
                        vertical-align: middle;
                        font-weight: 600;
                        color: blackColor;
                        letter-spacing: 2px;
                        &:nth-child(1) {
                            margin-right: 20px;
                        }
                    }
                    .subTitle {
                        font-size: 28px;
                        line-height: 40px;
                        height: 40px;
                        padding: 0 10px;
                        color: white;
                        background-color: blackColor;
                        display: inline-block;
                        vertical-align: middle;
                        font-weight: 600;
                        margin-left: 14px;
                        -webkit-print-color-adjust: exact;
                        letter-spacing: 10px;
                    }
                }
                .options {
                    font-size: 0;
                    margin-top: 26px;
                    margin-bottom: 6px;
                    .item {
                        display: inline-block;
                        font-size: 16px;
                        vertical-align: text-bottom;
                        &:nth-child(1) {
                            width: (238 / 810 * 100)%;
                            position: relative;
                            .itemTitle {
                                padding-left: 6px;
                            }
                            .itemContent {
                                position: absolute;
                                left: 57px;
                                right: 0;
                                top: 0;
                                bottom: 0;
                                font-size: 0;
                                z-index: 1;
                                // cursor: pointer !important;
                                .el-date-editor {
                                    width: 100%;
                                    height: 100%;
                                    opacity: 0;
                                    position: absolute;
                                    z-index: 1;
                                    >>>input {
                                        height: 18px;
                                        line-height: 18px;
                                    }
                                }
                                .showDate {
                                    position: absolute;
                                    left: 0;
                                    top: 0;
                                    width: 100%;
                                    height: 100%;
                                    line-height: 18px;
                                    font-size: 0;
                                    .text {
                                        font-size: 15px;
                                        display: inline-block;
                                    }
                                    .number {
                                        font-size: 14px;
                                        display: inline-block;
                                        text-align: center;
                                        &.year {
                                            width: 58px;
                                        }
                                        &.month {
                                            width: 36px;
                                        }
                                        &.date {
                                            width: 36px;
                                        }
                                    }
                                }
                            }
                        }
                        &:nth-child(2), &:nth-child(3) {
                            width: 174px;
                            position: relative;
                            .itemTitle {
                                font-size: 25px;
                                font-weight: 600;
                            }
                            .itemContent {
                                position: absolute;
                                left: 70px;
                                right: 0;
                                top: 0;
                                bottom: 0;
                                input {
                                    width: 100%;
                                    height: 100%;
                                    border: none;
                                    text-align: center;
                                    font-size: 25px;
                                }
                            }
                        }
                        &:nth-child(4) {
                            width: 100px;
                            margin-left: 37px;
                            position: relative;
                            .itemTitle {
                                font-size: 22px;
                                font-weight: 600;
                            }
                            .itemContent {
                                position: absolute;
                                left: 50px;
                                right: 0;
                                top: 50%;
                                bottom: 0;
                                transform: translate(0, -50%);
                                width: 136px;
                                height: 100%;
                                input {
                                    position: absolute;
                                    top: 50%;
                                    left: 0;
                                    transform: translate(0, -50%);
                                    width: 136px;
                                    height: 100%;
                                    border: none;
                                    text-align: center;
                                    font-size: 30px;
                                    height: 30px;
                                    color: red;
                                    text-align: left;
                                }
                            }
                        }
                    }
                }
            }
            .body {
                text-align: left;
                .row {
                    font-size: 0;
                    .col {
                        display: inline-block;
                        vertical-align: text-top;
                    }
                }
                >.row {
                    // white-space: nowrap;
                    >.col {
                        &:nth-child(1) {
                            width: 600px;
                            >.row {
                                &:nth-child(1) {
                                    >.col {
                                        &:nth-child(1) {
                                            border: 1px solid blackColor;
                                            width: 104px;
                                            height: 77px;
                                            line-height: 20px;
                                            position: relative;
                                            border-right: none;
                                            h4 {
                                                position: absolute;
                                                left: 50%;
                                                top: 50%;
                                                transform: translate(-50%, -50%);
                                                white-space: nowrap;
                                                font-size: 16px;
                                            }
                                        }
                                        &:nth-child(2) {
                                            border: 1px solid;
                                            border-right: none;
                                            width: 140px;
                                            height: 77px;
                                            position: relative;
                                            input {
                                                width: 100%;
                                                height: 100%;
                                                line-height: 77px;
                                                border: none;
                                                text-align: center;
                                                font-size: 16px;
                                                font-size: 25px;
                                            }
                                        }
                                        &:nth-child(3) {
                                            border: 1px solid;
                                            border-right: none;
                                            width: 54px
                                            height: 77px;
                                            text-align: center;
                                            >div {
                                                height: 50%;
                                                font-size: 16px;
                                                line-height: (77 / 2)px;
                                                &:nth-child(1) {
                                                    border-bottom: 1px solid;
                                                }
                                            }
                                        }
                                        &:nth-child(4) {
                                            border: 1px solid;
                                            border-right: none;
                                            width: 302px;
                                            height: 77px;
                                            .phone, .address {
                                                height: 50%;
                                                font-size: 16px;
                                                line-height: (77 / 2)px;
                                                position: relative;
                                                input {
                                                    position: absolute;
                                                    width: 100%;
                                                    height: 100%;
                                                    left: 0;
                                                    top: 0;
                                                    border: none;
                                                    font-size: 16px;
                                                    padding: 0 12px;
                                                }
                                                &:nth-child(1) {
                                                    border-bottom: 1px solid;
                                                }
                                            }
                                        }
                                    }
                                }
                                &:nth-child(2), &:nth-child(3), &:nth-child(4) {
                                    text-align: left;
                                    >.col {
                                        height: 50px;
                                        font-size: 16px;
                                        line-height: 38px;
                                        text-align: center;
                                        overflow: hidden;
                                        height: 38px;
                                        // border: 1px solid red !important;
                                        &:nth-child(1) {
                                            width: 134px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                        }
                                        &:nth-child(2) {
                                            width: 110px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                            .el-select {
                                                >>>input {
                                                    height: 38px;
                                                    line-height: 38px;
                                                    font-size: 16px;
                                                }
                                            }
                                        }
                                        &:nth-child(3) {
                                            width: 54px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                        }
                                        &:nth-child(4) {
                                            width: 75px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                        }
                                        &:nth-child(5) {
                                            width: 75px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                            cursor: pointer;
                                        }
                                        &:nth-child(6) {
                                            width: 75px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                            cursor: pointer;
                                        }
                                        &:nth-child(7) {
                                            width: 77px;
                                            border: 1px solid;
                                            border-top: none;
                                            border-right: none;
                                            cursor: pointer;
                                        }
                                        .el-icon-check {
                                            font-size: 40px;
                                        }
                                        input {
                                            width: 100%;
                                            height: 100%;
                                            line-height: 38px;
                                            font-size: 16px;
                                            text-align: center;
                                            border: none;
                                        }
                                    }
                                }
                                &:nth-child(5) {
                                    border: 1px solid;
                                    border-top: none;
                                    border-right: none;
                                    height: 37px;
                                    line-height: 37px;
                                    text-align: left;
                                    overflow: hidden;
                                    position: relative;
                                    .amount {
                                        height: 37px;
                                        .text {
                                            font-size: 16px;
                                            display: inline-block;
                                            width: 72px;
                                            text-align: right;
                                            vertical-align: middle;
                                        }
                                        input {
                                            width: 220px;
                                            height: 37px;
                                            line-height: 37px;
                                            vertical-align: middle;
                                            border: none;
                                            font-size: 16px;
                                            padding: 0 12px;
                                        }
                                    }
                                    .cost {
                                        position: absolute;
                                        right: 0;
                                        top: 0;
                                        width: 210px;
                                        height: 37px;
                                        top: 0;
                                        right: 0;
                                        font-size: 0;
                                        white-space: nowrap;
                                        .text {
                                            font-size: 16px;
                                            display: inline-block;
                                            vertical-align: middle;
                                        }
                                        input {
                                            width: 106px;
                                            height: 37px;
                                            line-height: 50px;
                                            vertical-align: middle;
                                            border: none;
                                            padding: 0 12px;
                                            font-size: 16px;
                                        }
                                    }
                                }
                                &:nth-child(6) {
                                    font-size: 0;
                                    text-align: left;
                                    border-bottom: 1px solid;
                                    .totalTitle {
                                        display: inline-block;
                                        height: 38px;
                                        width: 106px;
                                        border: 1px solid;
                                        border-top: none;
                                        border-bottom: none;
                                        text-align: center;
                                        position: relative;
                                        vertical-align: middle;
                                        >div {
                                            position: absolute;
                                            left: 50%;
                                            top: 50%;
                                            transform: translate(-50%, -50%);
                                            h4 {
                                                line-height: 24px;
                                                font-size: 18px;
                                                white-space: nowrap;
                                            }
                                            span {
                                                font-size: 14px;
                                                white-space: nowrap;
                                            }
                                        }
                                    }
                                    .totalContent {
                                        display: inline-block;
                                        width: 490px;
                                        font-size: 0;
                                        white-space: nowrap;
                                        position: relative;
                                        vertical-align: middle;
                                        padding-left: 4px;
                                        .item {
                                            display: inline-block;
                                            width: 66px;
                                            vertical-align: middle;
                                            .text {
                                                font-size: 16px;
                                                line-height: 38px;
                                            }
                                            input {
                                                display: inline-block;
                                                width: 74px;
                                                height: 38px;
                                                line-height: 38px;
                                                text-align: center;
                                                font-size: 16px;
                                                text-align: center;
                                                border: none;
                                            }
                                        }
                                        .capitalizedNumber {
                                            height: 38px;
                                            overflow: hidden;
                                            .el-select {
                                                width: 51px;
                                                >>>.el-input__suffix {
                                                    display: none;
                                                }
                                                >>>input {
                                                    height: 38px;
                                                    text-align: center;
                                                    border: none;
                                                    line-height: 38px;
                                                    font-size: 16px;
                                                    color: blackColor;
                                                    padding-right: 15px;
                                                }
                                            }
                                        }
                                        .number {
                                            position: absolute;
                                            right: 0;
                                            top: 0;
                                            i {
                                                font-size: 16px;
                                                vertical-align: middle;
                                            }
                                            input {
                                                width: 100px;
                                                vertical-align: middle;
                                                height: 38px;
                                                line-height: 38px;
                                                // padding: 0 12px;
                                                border: none;
                                                font-size: 16px;
                                            }
                                        }
                                    }
                                }
                            }
                        }
                        &:nth-child(2) {
                            width: 210px;
                            .markTitle {
                                line-height: (77 / 2)px;
                                height: (77 / 2)px;
                                border: 1px solid;
                                font-size: 16px;
                                text-align: center;
                            }
                            .mark {
                                display: block;
                                resize: none;
                                width: 100%;
                                height: 189px;
                                border: 1px solid;
                                border-top: none;
                                font-size: 16px;
                                text-align: left;
                                padding: 12px;
                                font-family: Microsoft Yahei;
                            }
                            >.row {
                                border: 1px solid;
                                border-top: none;
                                text-align: left;
                                font-size: 0;
                                .personalTitle {
                                    width: 68px;
                                    height: 38px;
                                    line-height: 38px;
                                    font-size: 16px;
                                    display: inline-block;
                                    border-right: 1px solid;
                                    text-align: center;
                                    vertical-align: middle;
                                }
                                input {
                                    display: inline-block;
                                    height: 38px;
                                    vertical-align: middle;
                                    width: 140px;
                                    border: none;
                                    text-align: center;
                                    font-size: 16px;
                                    text-align: left;
                                    padding: 0 12px;
                                }
                            }
                        }
                    }
                }
                .packing {
                    position: relative;
                    .el-select {
                        position: absolute;
                        width: 100%;
                        height 100%;
                        left: 0;
                        top: 0;
                        >>>.el-input__suffix {
                            display: none;
                        }
                        >>>input {
                            height: 50px;
                            font-size: 25px;
                            color: blackColor;
                            text-align: center;
                            border: none;
                        }
                    }
                }
                .otherInfo {
                    border: 1px solid;
                    border-top: none;
                    padding: 4px 0;
                    .item {
                        line-height: 14px;
                        .title {
                            display: inline-block;
                            font-size: 16px;
                            width: 48px;
                            padding-left: 4px;
                        }
                        .content {
                            font-size: 12px;
                            letter-spacing: 1px;
                        }
                    }
                }
            }
            .footer {
                padding-top: 4px;
                .row {
                    &:nth-child(1) {
                        .item {
                            display: inline-block;
                            line-height: 22px;
                            &:nth-child(1) {
                                width: 580px;
                            }
                            &:nth-child(2) {
                                width: 230px;
                            }
                            span {
                                display: inline-block;
                                font-size: 18px;
                                &:nth-child(1) {
                                    padding-left: 4px;
                                }
                            }
                        }
                    }
                    &:nth-child(2) {
                        .item {
                            display: inline-block;
                            line-height: 22px;
                            &:nth-child(1) {
                                width: 273px
                            }
                            &:nth-child(2) {
                                width: 308px;
                            }
                            &:nth-child(3) {
                                width: ((1088 - 800) / 1088 * 100)%;
                            }
                            span {
                                display: inline-block;
                                font-size: 18px;
                                &:nth-child(1) {
                                    padding-left: 4px;
                                }
                            }
                        }
                    }
                }
            }
        }
        .control {
            position: fixed;
            right: 0;
            bottom: 0;
            background-color: transparent;
            // box-shadow: 0 -5px 10px rgba(0, 0, 0, 0.05);
            padding: 10px 0;
            width: 100%;
            text-align: center;
            background-color: white;
            border-top: 1px solid rgba(0, 0, 0, 0.25);
            .item {
                display: inline-block;
                margin: 0 20px;
                .itemTitle {
                    display: inline-block;
                    width: 90px;
                    font-size: 14px;
                    vertical-align: middle;
                    text-align: right;
                    margin-right: 20px;
                }
                .itemContent {
                    display: inline-block;
                    width: 200px;
                    vertical-align: middle;
                    margin-right: 30px;
                    white-space: nowrap;
                    .el-slider {
                        display: inline-block;
                        width: 200px;
                        vertical-align: middle;
                        margin-right: 10px;
                    }
                    input {
                        display: inline-block;
                        width: 50px;
                        vertical-align: middle;
                        border: 1px solid rgba(0, 0, 0, 0.25);
                        border-radius: 4px;
                        text-align: center;
                    }
                }
            }
        }
    }
</style>
