<template>
    <div id="message-window">
        <div class="chat-container">
            <Message
                    v-for="message in sortedMessages"
                    :key="message.id"
                    :message="message"
                    :currentUser="currentUser"
            ></Message>
        </div>
        <MessageInput @sendMessage="sendMessage"></MessageInput>
    </div>
</template>

<script>
    import Message from './Message.vue';
    import MessageInput from './MessageInput.vue'

    export default {
        name: 'MessageWindow',
        components: {
            Message,
            MessageInput
        },
        data() {
            return {
                messagesList: [
                    {
                        text: 'what? you think you\'re tumblr?',
                        timestamp: 1530023681,
                        user: 'bob123',
                        id: 1,
                        isRead: true,
                        toShowDetails: false
                    },
                    {
                        text: 'no time to explain!',
                        timestamp: 1530123984,
                        user: 'me',
                        id: 2,
                        isRead: true,
                        toShowDetails: false
                    },
                    {
                        text: 'i\'m listening',
                        timestamp: 1530135094,
                        user:'bob123',
                        id: 3,
                        isRead: false,
                        toShowDetails: false
                    },
                    {
                        text: 'speak',
                        timestamp: 1530135194,
                        user: 'bob123',
                        id: 4,
                        isRead: false,
                        toShowDetails: false
                    }
                ],
                currentUser: 'me',
                newMessage: {}
            }
        },
        computed: {
            sortedMessages: function () {
                return this.messagesList.sort((a, b) => {
                    this.sort(a, b);
                })
            }
        },
        methods: {
            messageComparison: function () {
                for (var i = 0; i < this.messagesList.length; i++) {
                    if (i === 0) {
                        this.messagesList[i].toShowDetails = true;
                    } else {
                        if (this.messagesList[i].user !== this.messagesList[i - 1].user) {
                            this.messagesList[i].toShowDetails = true;
                        }
                    }
                }
            },
            checkForNew: function () {
                for (let i = 0; i < this.messagesList.length; i++) {
                    if (this.messagesList[i].isRead === false) {
                        if (this.messagesList[i].user === this.messagesList[i - 1].user) {
                            for (let x = 1; x <= i; x++) {
                                if (this.messagesList[i].user === this.messagesList[i - x].user) {
                                    this.messagesList[i].isRead = true;
                                }
                            }
                        }
                    }
                }
            },
            sendMessage: function (data) {
                if (data !== '') {
                    this.newMessage = data;
                    this.newMessage.id = this.messagesList.length + 1;
                    this.messagesList.push(this.newMessage);
                    this.allBeforeRead();
                }
            },
            allBeforeRead() {
                    this.messagesList.forEach(function (message) {
                        message.isRead = true;
                    })
            },
            sort(a, b) {
                if (a.timestamp > b.timestamp) {
                    return -1;
                } else {
                    return 1;
                }
            }
        },
        mounted() {
            this.messageComparison();
            this.checkForNew();
        },
        updated() {
            this.$nextTick(function () {
                this.messageComparison();
                this.checkForNew();
            })
        }
    }
</script>

<style lang="scss">
    #message-window {
        background: #C9CCD3;
        background-image: linear-gradient(-180deg, rgba(255,255,255,0.50) 0%, rgba(0,0,0,0.50) 100%);
        background-blend-mode: lighten;
        width: calc(100% - 250px);
        height: 100vh;
        display: inline-block;

        .chat-container {
            max-height: 90vw;
            overflow: auto;
        }
    }
</style>