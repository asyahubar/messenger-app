<template>
    <div id="message-input">
        <form action="" @submit.prevent="formGetSubmitted">
            <textarea cols="30" rows="2" autofocus v-model="inputText"></textarea>
            <button
                    @click="$emit('sendMessage', newMessage)"
                    :disabled="allowSend"
            >Send</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'MessageInput',
        data() {
            return {
                inputText: ''
            }
        },
        computed: {
            newMessage() {
                return {
                    text: this.inputText,
                    timestamp: this.moment(),
                    user: 'me',
                    id: 0,
                    isRead: true,
                    toShowDetails: false
                }
            },
            allowSend() {
                return this.inputText === '' ? true : false;
            }
        },
        methods: {
            formGetSubmitted() {
                this.inputText = "";
            }
        }
    }
</script>

<style lang="scss">
    #message-input {
        position: absolute;
        right: 0;
        bottom: 0;
        height: 6vh;
        width: calc(100vw - 266px);
        background-color: rgba(0, 0, 0, 0.2);
        box-sizing: content-box;
        padding: 10px 8px;

        form {
            display: flex;
            align-items: center;
            justify-content: space-between;

            textarea {
                width: calc(92vw - 266px);
                max-height: 9vh;
                padding: 14px 10px;
                resize: none;
                background-color: #C9CCD3;
                border-radius: 10px;
                outline: none;

                &:focus-within {
                    background-color: white;
                }
            }

            button {
                width: 50px;
                height: 50px;
                border-radius: 50%;
                background-color: royalblue;
                border-color: royalblue;
                cursor: pointer;
            }
        }
    }
</style>