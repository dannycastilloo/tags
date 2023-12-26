<script>
export default {
    emits: ["onTagsChange"],
    data() {
        return {
            currentValue: '',
            tags: [],
        }
    },
    methods: {
        handleKeyDown(e) {
            if (e.key === 'Backspace' && this.currentValue === '') {
                this.tags.pop()
                //this.onTagsChange(this.tags)
                this.$emit('onTagsChange', this.tags)
            }
        },
        handleSubmit() {
            if (this.currentValue !== '') {
                const exist = this.tags.some(item => item === this.currentValue)
                if (!exist) {
                    this.tags.push(this.currentValue)
                    this.currentValue = ''
                    //this.onTagsChange(this.tags)
                    this.$emit('onTagsChange', this.tags)
                }
            }
        },
        deleteTag(tag) {
            this.tags = this.tags.filter((item) => item !== tag)
            //this.onTagsChange(this.tags)
            this.$emit('onTagsChange', this.tags)
        }
    }
}
</script>

<template>
    <div class="input-tag">
        <div class="tags">
            <div class="tag" v-for="(tag, index) in tags" :key="index">
                {{ tag }} <button @click="deleteTag(tag)">X</button>
            </div>
        </div>
        <form @submit.prevent="handleSubmit">
            <input class="input" type="text" v-model="currentValue" @keydown="handleKeyDown">
        </form>
    </div>
</template>

<style scoped>
.input-tag {
    display: inline-flex;
    border: 1px solid #000;
    border-radius: 4px;
    height: 43px;
}

.tags {
    display: flex;
    gap: 3px;
    padding: 5px;
}

.tags .tag {
    display: flex;
    padding: 5px;
    border: 1px solid #ccc;
    gap: 5px;
    align-items: center;
    border-radius: 4px;
}

.input-tag form {
    display: inline-flex;
}

.input-tag .input {
    border: none;
    outline: none;
    padding: 0 5px;
}

.input-tag button {
    background-color: transparent;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.input-tag button:hover {
    background-color: #eee;
}
</style>