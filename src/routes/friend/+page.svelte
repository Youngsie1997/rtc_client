<script>
  import { Peer } from "peerjs";
  var friendId = "pineapple-sunglasses";
  var peer;
  var message = "hello world";
  var conn;

  function connect() {
    peer = new Peer("pineapple-testicles", { debug: 3 });
    peer.on("connection", function (conn) {
      conn.on("data", function (data) {
        console.log(data);
      });
    });

    conn = peer.connect(friendId);
    // on open will be launch when you successfully connect to PeerServer
    conn.on("open", function () {
      console.log("sending message");
      conn.send("Made contact");
      console.log(conn.id);
    });
  }

  function sendMessage() {
    conn = peer.connect(friendId);
    conn.on("open", function () {
      conn.send(message);
    });
  }
</script>

<h1>WebRtc Client</h1>

<button on:click={sendMessage}>Send Message</button>
<button on:click={connect}>Connect</button>
<br />

<label for="messageBox">Message</label>
<input type="text" id="messageBox" bind:value={message} />
<br />
<label for="friendID">Friend</label>
<input type="text" bind:value={friendId} />
