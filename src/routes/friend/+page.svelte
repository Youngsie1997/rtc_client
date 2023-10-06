<script>
  import { Peer } from "peerjs";
  const friendId = "pineapple-sunglasses";
  const peer = new Peer("pineapple-testicles");

  function sendMessage() {
    peer.on("connection", function (conn) {
      conn.on("data", function (data) {
        console.log(data);
      });
    });

    var conn = peer.connect(friendId);
    // on open will be launch when you successfully connect to PeerServer
    conn.on("open", function () {
      console.log("sending message");
      conn.send("Hello earthlings!");
      console.log(conn.id);
    });
  }
</script>

<h1>WebRtc Client</h1>

<button on:click={sendMessage}>Deploy Missle!</button>
