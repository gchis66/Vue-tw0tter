<template>
    <div class="tw33t-item" @click="favoriteTw33t(tw33t.id)">
        <div class="user-profile_tw33t">
            <div class="tw33t-item_user">
                @{{username}}
            </div>
            <div class="tw33t-item_content">
                {{tw33t.content}}
            </div>
        </div>
    </div>

</template>

<script>
export default {
    name: "Tw33tItem",
    props: {
        username: {
            type: String,
            required: true
        },
        tw33t: {
            type: Object,
            required: true
        }
    },
    methods: {
        favoriteTw33t(id) {
            this.$emit('favorite', id)
        }
    }
};
</script>

<style scoped>

.tw33t-item {
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease;
    margin-bottom: 10px;
}
.tw33t-item:hover {
    transform: scale(1.1, 1.1);
}
.tw33t-item_user{
    font-weight: bold;
}

</style>