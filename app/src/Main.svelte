<script>
    import { onMount } from "svelte";


    export let name;
    export let SERVER;
    export let DEBUG;

    let currentMsg="";
    let users = ['you', 'them', 'someone else'];
    let messages = [
        {
            sender: name,
            msg: "wassup"
        },
        {
            sender: "them",
            msg: "smol pp"
        },
        {
            sender: name,
            msg: "o sorry"
        }
    ];

    function sendMessage() {
        let message = {
            sender: name,
            msg: currentMsg
        };
        messages = [...messages, message];
        currentMsg = "";
    }

    function sendBoxKeypress(event) {
        if (event.key === "Enter") { sendMessage(); }
    }

    let sendBox;

    onMount(function() {
        sendBox.focus();
    });
</script>

<style>
    #sidebar {
        width: 10%;
        position: fixed;
        height: 100%;
        z-index: 1;
        top: 0;
        left: 0;
        background-color: rgb(49, 49, 49);
        overflow-x: hidden;
        padding-top: 20px;
        color:rgb(255, 255, 255);
    }
    #users {
        position: absolute;
        left: 10px;
    }
    .me {
        color:rgb(5, 143, 185);
    }
    #info {
        position: absolute;
        bottom: 10px;
        left: 10px;
    }

    #messageArea {
        position: fixed;
        left: 10%;
        width: 85%;
        height: 100%;
    }

    #messages {
        position: absolute;
        left: 10%;
        top: 0%;
        height: 90%;
        width: 90%;
    }
    .message {
        position: absolute;
        font-size: 15px;
        height: 15px;
        width: 100%;
    }
    .messageSenderNotMe {
        color:rgb(49, 49, 49);
    }

    #messageControls {
        position: relative;
        margin: auto;
        top: 90%;
        width: 80%;
        height: 5%;
    }
    #messageInput {
        border-style: solid;
        border-width: 4px;
        position: absolute;
        width: 88%;
        height: 100%;
        left: 0;
    }
    #messageSend {
        position: absolute;
        width: 8%;
        height: 100%;
        right: 0;
    }

</style>

<div id = "sidebar">

    <div id = "users">
        <p class = "me">{name}</p>
        {#each users as user}
        <p>{user}</p>
        {/each}
    </div>

    {#if DEBUG}
    <div id = "info">
        <p>Name: <span class = "me">{name}</span></p>
        <p>Server: {SERVER}</p>
    </div>
    {/if}

</div>

<div id = "messageArea">
    <div id = "messages">

        {#each messages as message}
        <div class = "message" style = "bottom: {(messages.length - messages.indexOf(message)) * 50}px;">

            {#if message.sender === name}
            <span class = "me">{message.sender}: </span>
            {:else}
            <span class = "messageSenderNotMe">{message.sender}: </span>
            {/if}
            
            <span class = "messageText">{message.msg}</span>
        </div>
        {/each}
        
    </div>

    <div id = "messageControls">
        <input bind:value = {currentMsg} type = "text" id = "messageInput" on:keydown={sendBoxKeypress} bind:this = {sendBox}/>
        <button on:click = {sendMessage} id = "messageSend">Send</button>
    </div>

</div>