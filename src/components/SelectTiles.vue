<template>
    <div class="select-tiles">
        <div :class="className">
            <label class="select-tiles__title" v-if="$slots.label"><slot name="label"></slot></label>
            <slot name="header"></slot>
            <label
                class="select-tiles__label"
                v-for="(item, i) in items">

                <input
                       class="select-tiles__input"
                       :style="{display: isInputShow}"
                       :name="name"
                       :type="mode"
                       :id="item[idKey]"
                       :value="item[valueKey]"
                       v-model="tmp"
                       @change="updateSelected">


                <div class="select-tiles__btn">
                    <span class="select-tiles__btn-text">{{item[textKey]}}</span>
                    <span class="select-tiles__btn-secondText" v-if="secondTextKey" >{{item[secondTextKey]}}</span>
                </div>

            </label>
        </div>
    </div>
</template>

<script>
    import linq from 'linq'

    export default {
        name: 'select-tiles',

        data() {
            return {
                tmp: [],
                pick: null
            }
        },

        computed: {
            isInputShow() {
                return(this.inputShow)? '' : 'none'
            }
        },

        model: {
            prop: 'selected',
            event: 'change'
        },

        props: {
            name: {
                type: String
            },
            mode: {
                type: String,
                default: 'checkbox',
                validator: function (value) {
                    return ['checkbox', 'radio'].indexOf(value) !== -1
                }
            },
            textKey: {
                default: 'value',
            },
            valueKey: {
                default: 'value'
            },
            idKey: {
                default: 'id'
            },
            items: {
                type: Array,
                required: true
            },
            selected: {
                type: Array
            },
            inputShow: Boolean,
            old: {
                type: Array,
                default: []
            },
            secondTextKey: {
                type: String
            },
            className: {
                type: String
            }
        },
        created() {
            if(this.mode == 'checkbox' && this.old) {
                linq.from(this.old).forEach((x, i) => {
                    this.$set(this.selected, i, x)
                    this.$set(this.tmp, i, x)
                })
            }
            if(this.mode == 'radio' && this.old) {
                this.tmp = this.old[0]
                this.$set(this.selected, 0, this.tmp)
            }
        },
        methods: {
            updateSelected(e) {
                const check = e.target.checked
                const value = e.target.value

                this.$emit('checkStatus', check, this.tmp);

                if(this.mode === 'radio') {
                    //radioボタンの時
                    this.$set(this.selected, 0, this.tmp)
                } else if(check) {
                    //checkboxの時
                    linq.from(this.tmp).forEach((x, i) => {
                        this.$set(this.selected, i, x)
                    })
                } else {
                    linq.from(this.selected).forEach((x, i) => {
                        if(x == value) {
                            this.$delete(this.selected,i,x)
                        }
                    })
                }
            }
        }
    }
</script>


