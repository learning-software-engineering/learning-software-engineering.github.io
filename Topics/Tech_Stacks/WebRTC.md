# WebRTC

## Introduction

You may be wondering how web applications like Google Meet enables video chat functionality, third-party APIs? Turns out that modern browsers has a native set of APIs that enables peer-to-peer communications, called [WebRTC](https://webrtc.org). You may be curious about what WebRTC is and its application in integrating video chat into web applications. Allow me to guide you through its basics and uses.

WebRTC equips both browsers and mobile apps with the capability of real-time communication (RTC) through straightforward APIs. A standout characteristic of WebRTC is its peer-to-peer architecture, which enables data transmission directly between users, bypassing the need for a server. This approach significantly boosts both speed and efficiency.


## Signaling Server

In order to establish a peer-to-peer connection, you will first need a central server so that the peers could communicate first. The signalling server essentially acts as a proxy, user send activities to it and it will broadcast to the rest of the peers as signals. This is usually achieved with [WebSocket](https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/). For example, when a user joins a room, the user makes a request to the server and then is broadcasted with the peers, so the peers within the same channels are notified that the user has joined.

Example signal
```
{
  type: "EXCHANGE",
  from: userId,
  to: otherUserId,
  sdp: JSON.stringify(pc.localDescription),
}
```
## ICE candidates

You might be wondering now why do we need a signaling server? The peer-to-peer connection can only be established after the peers have exchanged their ICE candidates, and that's why we need a signaling server. ICE (Interactive Connectivity Establishment) is an essential part of WebRTC that enables real-time communication even in the face of complex network scenarios. An ICE candidate is a potential method that two peers on a WebRTC session can use to communicate. Each candidate is a combination of a transport address (a combination of IP address and a port number), a transport protocol (usually UDP or TCP), and a type that reflects the candidate's network topology.

ICE candidates are collected for each type of media in the connection (be it audio, video, or data). The process of gathering these candidates is known as "ICE gathering."

There are three primary types of ICE candidates:

 * **Host Candidates:** These candidates use IP addresses from the device’s own network interfaces, like Wi-Fi or Ethernet. They offer the most straightforward connection paths between peers. However, they might be unusable in situations where a direct peer-to-peer connection is hindered by firewalls or NAT (Network Address Translation).
 * **Server Reflexive Candidates:** These candidates represent the external addresses of a NAT. They are determined by interacting with a STUN (Session Traversal Utilities for NAT) server. In this process, the client sends a request to the STUN server, which then responds with the public IP address and port that it sees for the client.
 * **Relayed Candidates:** In scenarios where both direct connections and STUN methods fail, communication between peers may occur through a TURN (Traversal Using Relays around NAT) server. This server acts as an intermediary, relaying media between the peers. This method is more resource-demanding and is generally considered a fallback option.

Once a peer gathers an ICE candidate, it sends a message over the signaling channel to the other peer. This message includes the candidate's transport address, protocol, and type. The receiving peer adds the candidate to its RTCPeerConnection by calling the addIceCandidate() method. The process continues until all candidates have been gathered and sent to the other peer.

Ex: Broadcasting your ICE candidates
```javascript
peerConnection.addEventListener('icecandidate', event => {
    if (event.candidate) {
      this.signalingChannel.send({
        type: EXCHANGE,
        from: userId,
        to: otherUserId,
        sdp: JSON.stringify(event.candidate),
      })
    }
});
```

## STUN and TURN servers

STUN and TURN servers play a crucial role in ICE:

* **STUN Servers:** A STUN server is used to discover the public IP/port, which is necessary to generate server reflexive candidates. It's also used in connectivity checks to punch holes in firewalls and NATs.
* **TURN Servers:** A TURN server is used when direct connection and STUN are unsuccessful, usually due to network restrictions. It acts as a relay, forwarding media between peers. Relayed candidates are the least preferred due to their high usage of bandwidth and processing power.

Why you need a TURN server? Sometimes, you will need a server in between to bypass restrictions such as firewalls. This is common if a user is on Cellular as opposed to Wi-Fi where Cellular has more restrictions. Thus the connection has to be established through a TURN server as it usually runs on port 80 or 443 to bypass the restrictions. There are several solutions on the internet, but they all come with a cost. There is a way around this is to host your own TURN server with [coturn](https://github.com/coturn/coturn).

![turn-server-21d0a088ff33ba667aa62b5101226d57-2](https://github.com/davidlin2k/learning-software-engineering.github.io/assets/17074619/d662b500-8445-43be-ba21-ed92484bb021)
Image from https://www.metered.ca/tools/openrelay/assets/images/turn-server-21d0a088ff33ba667aa62b5101226d57.png

## Signalling and Establishing Connection

Establishing a WebRTC connection involves several steps and operations. [Here](https://webrtc.org/getting-started/peer-connections)'s a more detailed explanation of each step.

## Streaming

After the connection is established and say you receive the stream from the other user, this is where the on ontrack event handler comes in place. With the event handler, you can now start streaming audio and video between the peers.

```
const remoteVideo = document.querySelector('#remoteVideo');

peerConnection.addEventListener('track', async (event) => {
    const [remoteStream] = event.streams;
    remoteVideo.srcObject = remoteStream;
});
```

Example from https://webrtc.org/getting-started/remote-streams
