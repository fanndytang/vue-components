<template>
    <div></div>
</template>

<script>
    export default {
        install (Vue, options) {
            // 注册一个全局自定义指令 `v-loading`
            Vue.directive('loading', {
                inserted (el, binding, vnode, oldVnode) {
                    el.className = `${el.className} loading-box`
                    // let type = Object.prototype.toString.call(binding.value).toLocaleLowerCase()
                    //   let show = type === '[object object]' ? binding.value.load : binding.value  此种写法貌似直接在浏览器里取不到value
                    //   let msg = type === '[object object]' ? binding.value.msg : '加载中'
                    binding.value = binding.value || {}
                    let show = binding.value.load || false
                    let msg = binding.value.msg || '加载中'

                    let tpl = Vue.extend({
                        template: `<div class="loading ${show ? 'open' : ''}"><div><span class="icon-load"></span>${msg}</div></div>`
                    })
                    el.appendChild(new tpl().$mount().$el)
                },
                update (el, binding, vnode, oldVnode) {
                    let show = binding.value
                    let type = Object.prototype.toString.call(binding.value).toLocaleLowerCase()
                    if(type === '[object object]') show = binding.value.load
                    let $load = el.querySelector('.loading')
                    $load.className = $load.className.replace('open', '') + (show ? 'open' : '')
                }
            })
        }
    }
</script>

<style lang="less" scoped>
    .loading-box {
        position: relative;
        .loading {
            height: 100%;
            width: 100%;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 5000;
            background: rgba(255, 255, 255, .9);
            color: #20a0ff;
            text-align: center;
            display: none;
            &.open {
                display: flex;
                align-items: center;
                justify-content: center;
            }
        }
        .icon-load {
            display: block;
            width: 40px;
            height: 40px;
            border: 2px solid #20a0ff;
            border-top-color: transparent;
            margin: 5px auto;
            border-radius: 50%;
            animation: circle 1s infinite;
        }
    }

    @keyframes circle {
        0% {transform: rotate(0)}
        100% {transform: rotate(360deg)}
    }
</style>