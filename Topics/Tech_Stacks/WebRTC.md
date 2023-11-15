# WebRTC

## Introduction

You may be wondering how web applications like Google Meet enables video chat functionality, third-party APIs? Turns out that modern browsers has a native set of APIs that enables peer-to-peer communications, called WebRTC. You may be curious about what WebRTC is and its application in integrating video chat into web applications. Allow me to guide you through its basics and uses.

WebRTC equips both browsers and mobile apps with the capability of real-time communication (RTC) through straightforward APIs. A standout characteristic of WebRTC is its peer-to-peer architecture, which enables data transmission directly between users, bypassing the need for a server. This approach significantly boosts both speed and efficiency.

The workflow of a standard WebRTC application is quite structured. Initially, it captures the media of the user, such as video or audio. Following this, it locates other users to communicate with. Once found, it sends them a request to connect. After the other side agrees, a connection is established, paving the way for seamless data streaming. This process might seem simple at first glance, but it brings up an important query - how does one find and connect to other peers? This is where the concept of a signaling server becomes crucial, acting as a mediator in the discovery and connection process.
