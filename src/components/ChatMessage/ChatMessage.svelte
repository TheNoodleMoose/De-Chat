<script>
    export let message;
    export let sender;
    const messageClass = message.who === sender ? 'sent' : 'received';
    
    const avatar = `https://avatars.dicebear.com/api/initials/${message.who}.svg`;

    const ts = new Date(message.when);
</script>

<div class={`message ${messageClass}`}>
    <img src={avatar} alt="avatar" />
    <div class="message-text">
      <p>{message.what}</p>
  
      <time>{ts.toLocaleTimeString()}</time>
    </div>
</div>

<style>
  .message {
    display: flex;
    align-items: center;
    margin: 0;
    word-wrap: break-word;
  }

  .message:last-child {
    margin-bottom: 20px;
  }

  .sent {
    flex-direction: row-reverse;
  }

  .sent p {
    color: white;
    background: rgb(111, 40, 197);
    align-self: flex-end;
    text-align: right;
  }

  .received p {
    background: rgb(224, 222, 224);
    color: black;
    text-align: left;
  }

  .message-text {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }

  .received .message-text {
    align-items: flex-start;
  }

  time {
    color: white;
    font-size: 0.7rem;
    color: #9a9a9a;
    margin: 0 1rem;
  }
</style>