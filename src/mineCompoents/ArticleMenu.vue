<template>
    <div>
        <div class="menu-container">
            <div class="menu-bar">
                <div class="menu-item" :class="{ active: activeItem === 1 }" @click="selcetItem(1)">推荐</div>
                <div class="menu-item" :class="{ active: activeItem === 2 }" @click="selcetItem(2)">最新</div>
            </div>
        </div>
    </div>
</template>

<script>
import { useArticleStore } from '@/stores/article';
import { storeToRefs } from 'pinia';

export default ({
    setup() {
        const articleStore = useArticleStore();

        const { articleShowMethod } = storeToRefs(articleStore);
        const { setArticleShowMethod } = articleStore;

        return {
            articleShowMethod,
            setArticleShowMethod,
        }
    },

    data() {
        return {
            activeItem: 1,
            methods: ["recommend", "now"],
        }
    },
    methods: {
        //选择推荐还是最新的排序页面
        selcetItem(index) {
            this.activeItem = index;
            this.setArticleShowMethod(this.methods[index - 1]);
        }
    },
    mounted() {

    }
})

</script>

<style scoped>
.menu-bar {
    display: flex;
}

.menu-item {
    cursor: pointer;
    margin-right: 5px;
    border: 1px solid grey;
    padding: 5px 10px;
    border-radius: 5px;
}

.active {
    color: white;
    background-color: grey;
}
</style>