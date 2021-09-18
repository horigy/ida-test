<template>
    <div class="list-wrapper">
        <Select/>
        <ul class="list">
            <li v-for="(item, index) in items" :key="index" class="item">
                <img v-if="!item.img_link" src="../assets/img/default-img.png">
                <img v-else :src="item.img_link">
                <div class="item-info">
                    <h2>{{item.name}}</h2>
                    <p>{{item.desc}}</p>
                    <span>{{item.price}} руб.</span>
                </div>
                <img class="delete" src="../assets/delete.svg" @click="deleteItem(index)">
            </li>
        </ul>
    </div>
</template>

<script>
import Select from '@/components/Select.vue'
export default {
    components: {
        Select
    },
    data() {
        return {
            items: this.$store.getters.getItems,
        }
    },
    methods: {
        deleteItem(index) {
            this.$store.dispatch('deleteItem', index)
        }
    },
}
</script>

<style lang="scss" scoped>

.list-wrapper {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
}


.list {
    margin-top: 16px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
}

.item {
    max-width: 332px;
    height: 423px;
    position: relative;
    cursor: url(../assets/cursor.png), pointer;
    position: relative;
    display: flex;
    flex-direction: column;
}

.delete {
    position: absolute;
    top: -10px;
    right: -12px;
    width: 40px;
    height: 40px;
    display: none;

}

.item:hover > .delete {
    display: block;
}


.item-info {
    padding: 0 16px 24px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    text-align: left;
    flex: 1;
}

img {
    margin-bottom: 17px;
    max-width: 332px;
    height: 200px;
}

h2 {
    font-weight: 600;
    font-size: 20px;
    margin-bottom: 16px;
}

p {
    font-size: 16px;
    margin-bottom: 32px;
    line-height: 20px;
}

span {
    font-weight: 600;
    font-size: 24px;
    letter-spacing: 1px;
    margin-top: auto;
}
</style>