# Production

Nowadays, you can run JavaScript code in several different environments, some of them with their own particularities. Moreover, you can use `js-libp2p` for a wide range of use cases. Different environments and different use cases mean different configurations and challenges in the network.

Libp2p nodes can vary from nodes behind an application, to infrastructure nodes that enable the network to operate and to be efficient. In this context, the Libp2p project provides public infrastructure to boost the network, enable nodes connectivity and improve constrained nodes performance. This public infrastructure should be leveraged for learning the concepts and experimenting. When an application on top of libp2p aims to move into production, its own infrastructure should be setup as the public nodes will be intensively used by others and its availability is not guaranteed.

This guide aims to guide you from using the public infrastructure into setting up your own.

## Table of Contents

* [Production](#production)
  * [Star servers](#star-servers)
  * [Delegate nodes](#delegate-nodes)
  * [Circuit Relay](#circuit-relay)
  * [Rendezvous Server nodes](#rendezvous-server-nodes)

## `webrtc-star` servers

While the libp2p core codebase aims to work in multiple environments, there are some limitations that are not possible to overcome at the time of writing. Regarding `webRTC`, at the time of writing a set of star servers are needed to act as a rendezvous point, where peers can learn about other peers (`peer-discovery`), as well as exchange their SDP offers (signaling data).

You can read on how to setup your own set of delegated nodes in [STAR_SERVERS.md](./STAR_SERVERS.md).

It is worth pointing out that with new discovery protocols on the way, as well as support for distributed signaling, the star servers should be deprecated on the long run.

## Delegate nodes

Libp2p nodes in scenarios such as browser environment and constrained devices will not be an efficient node in the libp2p DHT overlay, as a consequence of their known limitations regarding connectivity and performance.

Aiming to support these type of nodes to find other peers and content in the network, delegate nodes can be setup. With a set of well known libp2p delegate nodes, nodes with limitations in the network can leverage them to perform peer and content routing calls.

You can read on how to setup your own set of delegated nodes in [DELEGATE_NODES.md](./DELEGATE_NODES.md).

## Circuit Relay

Libp2p nodes acting as circuit relay aim to establish connectivity between libp2p nodes (e.g. IPFS nodes) that wouldn't otherwise be able to establish a direct connection to each other.

A relay is needed in situations where nodes are behind NAT, reverse proxies, firewalls and/or simply don't support the same transports (e.g. go-libp2p vs. browser-libp2p). The circuit relay protocol exists to overcome those scenarios.

You can read on how to setup your own set of delegated nodes in [CIRCUIT_RELAY.md](./CIRCUIT_RELAY.md).

## Rendezvous Server nodes

The rendezvous protocol can be used in different contexts across libp2p. For using it, the libp2p network needs to have well known libp2p nodes acting as rendezvous servers. These nodes will have an extra role in the network. They will collect and maintain a list of registrations per rendezvous namespace. Other peers in the network will act as rendezvous clients and will register themselves on given namespaces by messaging a rendezvous server node. Taking into account these registrations, a rendezvous client is able to discover other peers in a given namespace by querying a server.

You can read on how to setup your own set of delegated nodes in [CIRCUIT_RELAY.md](./CIRCUIT_RELAY.md).
