<template>
    <div class="select form-input">
        <div class="select-field" @click="optionsVisible = !optionsVisible">
            {{selected}}
            <img class="select-arrow" :class="{'rotate': optionsVisible}" src="../assets/arrow.svg" alt="">
        </div>
        <div class="select-options" v-show="optionsVisible">
            <p class="select-option"
                v-for="(item, index) in regions"
                :key="index"
                @click="selectOption(item)"
            >{{item}}</p>
        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            optionsVisible: false,
            selected: 'По умолчанию',
            regions: [
                'по возрастанию',
                'по убыванию'
            ]
        }
    },
    methods: {
        selectOption(option) {
            this.selected = option
            this.optionsVisible = false
        }
    }
}
</script>

<style lang="scss">
.select {
    position: relative;
    font-size: 12px;
    line-height: 15px;
    color: #B4B4B4;
}
.select-field {
    width: 100%;
    height: 100%;
    cursor: pointer;
    padding: 10px 16px;
    border: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    min-width: 121px;
}
.select-options {
    position: absolute;
    z-index: 100;
    top: 107%;
    left: 0;
    width: 100%;
    max-height: 380px;
    overflow: hidden;
    overflow-y: scroll;
    background-color: #fff;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    min-width: 150px;
}
// .select-arrow {
//     position: absolute;
//     top: 50%;
//     transform: translateY(-25%) rotate(0);
//     right: 20px;
// }
.rotate {
    transform: translateY(-25%) rotate(180deg);
}
</style>