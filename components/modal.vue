<template>
    <div class="modal" v-show="value">
        <input type="hidden" :value="value" @input="value = $event.target.value">

        <div class="content">
            <span class="close" @click="$emit('input', false)">&times;</span>
            <div class="head">{{title}}</div>
            <div class="body">
                <slot></slot>
            </div>
            <div class="foot">
                <button class="btn btn-primary" type="button" @click="$parent.$emit('confirm')">确定</button>
                <button class="btn" type="button" @click="$emit('input', false)">取消</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            value: Boolean,
            title: String
        }
    }
</script>

<style lang="less" scoped>
    .modal {
        position: fixed;
        top: 0;
        left: 0;
        z-index: 100;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, .6);

        .content {
            width: 60%;
            height: 60%;
            background: #fff;
            border-radius: 10px;
            position: absolute;
            top: 15%;
            left: 20%;
            padding: 20px;
            display: flex;
            flex-direction: column;
        }

        .close {
            position: absolute;
            right: 0;
            top: 0;
            font-size: 24px;
            cursor: pointer;
            width: 30px;
            height: 30px;
            text-align: center;
            line-height: 30px;
            color: #bbb;
            &:hover {
                color: #20a0ff;
            }
        }

        .head {
            border-bottom: 1px solid #dcdfe6;
            line-height: 30px;
            text-align: center;
        }

        .body {
            flex: 1;
            overflow: auto;
        }

        .foot {
            border-top: 1px solid #dcdfe6;
            text-align: center;

            .btn {
                margin: 10px 10px 0 10px;
            }
        }
    }

    .btn {
        border: 1px solid #dcdfe6;
        background: transparent;
        font-size: 12px;
        padding: 3px 6px;
        border-radius: 3px;
        cursor: pointer;

        &.btn-primary {
            background: #20a0ff;
            border-color: #20a0ff;
            color: #fff;

            &:hover {
                background: #53b6ff;
                border-color: #53b6ff;
            }
        }
    }
</style>