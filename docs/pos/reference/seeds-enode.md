---
id: seeds-enode
title: Seeds & Enodes
sidebar_label: Seeds & Enodes
description: "A guide to essential Linux and Polygon-specific commands for node operations."
keywords:
  - docs
  - matic
  - polygon
  - validator
  - commands
  - faq
image: https://wiki.polygon.technology/img/polygon-logo.png
---

## Seeds

| Deployment Guide                                                                                   | Node Type | Network  | Seed Reference                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Full Node Binaries](/docs/pos/operate/node/full-node-binaries/)        | Full Node       | Mainnet  | `sed -i 's|^seeds =.*|seeds = "[email protected]:26656,6726b826df:26656"|g' /var/lib/heimdall/config/config.toml`                                                                                                       |
|                                                                                                        |                 | Mumbai   | Not explicitly mentioned in the provided content.                                                                                                                                                                                |
| [Full Node Ansible](/docs/pos/operate/node/full-node-ansible/)          | Full Node       | Mainnet  | `seeds "[email protected]:26656,:26656,67:26656"`                                                                                                                                                                                 |
|                                                                                                        |                 | Mumbai   | Not explicitly mentioned in the provided content.                                                                                                                                                                                |
| [Full Node Docker](/docs/pos/operate/node/full-node-docker/)            | Full Node       | Mainnet  | `seeds "LATEST LIST OF SEEDS"`                                                                                                                                                                                                   |
|                                                                                                        |                 | Mumbai   | Not explicitly mentioned in the provided content.                                                                                                                                                                                |
| [Run Validator Binaries](/docs/pos/validator/run-validator/run-validator-binaries/) | Validator Node      | Mainnet  | Heimdall seed nodes are mentioned but specific seed references are not provided in the visible content.                                                                                                                          |
| [Run Validator Ansible](/docs/pos/validator/run-validator/run-validator-ansible/)   | Validator Node       | Mainnet  | Heimdall seed nodes are mentioned but specific seed references are not provided in the visible content.                                                                                                                          |
| [Run Validator Packages](/docs/pos/validator/run-validator/run-validator-packages/) | Validator Node       | Mainnet  | Heimdall seed nodes are mentioned but specific seed references are not provided in the visible content.                                                                                                                          |

## Enodes

| Deployment Guide                                                                                   | Node Type | Network  | Enode Reference                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Full Node Binaries](/docs/pos/operate/node/full-node-binaries/)        | Full Node       | Mainnet  | `enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303` |
|                                                                                                        |                 | Mumbai   | `enode://bdcd4786a616a853b8a041f53496d853c68d99d54ff305615cd91c03cd56895e0a7f6e9f35dbf89131044e2114a9a782b792b5661e3aff07faf125a98606a071@43.200.206.40:30303` |
| [Full Node Ansible](/docs/pos/operate/node/full-node-ansible/)          | Full Node       | Mainnet  | `enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303` |
|                                                                                                        |                 | Mumbai   | `enode://bdcd4786a616a853b8a041f53496d853c68d99d54ff305615cd91c03cd56895e0a7f6e9f35dbf89131044e2114a9a782b792b5661e3aff07faf125a98606a071@43.200.206.40:30303` |
| [Full Node Docker](https://wiki.polygon.technology/docs/pos/operate/node/full-node-docker/)            | Full Node       | Mainnet  | `enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303` |
| [Validator Node Binaries](/docs/pos/validator/run-validator/run-validator-binaries/) | Validator Node       | Mainnet  | `enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303` |
| [Validator Node Ansible](/docs/pos/validator/run-validator/run-validator-ansible/)   | Validator Node       | Mainnet  | `enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303` |
| [Validator Node Packages](/docs/pos/validator/run-validator/run-validator-packages/) | Validator Node      | Mainnet  | `enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303` |



## RIGHT

| Deployment Guide URL                                                                                   | Deployment Type | Network  | Component | Seed Reference                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Full Node Binaries](https://wiki.polygon.technology/docs/pos/operate/node/full-node-binaries/)        | Full Node       | Mainnet  | Heimdall  | `sed -i 's|^seeds =.*|seeds = "1500161dd491b67fb1ac81868952be49e2509c9f@52.78.36.216:26656,dd4a3f1750af5765266231b9d8ac764599921736@3.36.224.80:26656,8ea4f592ad6cc38d7532aff418d1fb97052463af@34.240.245.39:26656,e772e1fb8c3492a9570a377a5eafdb1dc53cd778@54.194.245.5:26656,6726b826df45ac8e9afb4bdb2469c7771bd797f1@52.209.21.164:26656"|g' /var/lib/heimdall/config/config.toml` |
|                                                                                                        |                 | Mumbai   | Heimdall  | `sed -i 's|^seeds =.*|seeds = "9df7ae4bf9b996c0e3436ed4cd3050dbc5742a28@43.200.206.40:26656,d9275750bc877b0276c374307f0fd7eae1d71e35@54.216.248.9:26656,1a3258eb2b69b235d4749cf9266a94567d6c0199@52.214.83.78:26656"|g' /var/lib/heimdall/config/config.toml` |
|                                                                                                        |                 | Mainnet  | Bor       | `sed -i 's|.*bootnodes =.*|    bootnodes = ["enode://b8f1cc9c5d4403703fbf377116469667d2b1823c0daf16b7250aa576bacf399e42c3930ccfcb02c5df6879565a2b8931335565f0e8d3f8e72385ecf4a4bf160a@3.36.224.80:30303", "enode://8729e0c825f3d9cad382555f3e46dcff21af323e89025a0e6312df541f4a9e73abfa562d64906f5e59c51fe6f0501b3e61b07979606c56329c020ed739910759@54.194.245.5:30303"]|g' /var/lib/bor/config.toml` |
|                                                                                                        |                 | Mumbai   | Bor       | `sed -i 's|.*bootnodes =.*|    bootnodes = ["enode://bdcd4786a616a853b8a041f53496d853c68d99d54ff305615cd91c03cd56895e0a7f6e9f35dbf89131044e2114a9a782b792b5661e3aff07faf125a98606a071@43.200.206.40:30303", "enode://209aaf7ed549cf4a5700fd833da25413f80a1248bd3aa7fe2a87203e3f7b236dd729579e5c8df61c97bf508281bae4969d6de76a7393bcbd04a0af70270333b3@54.216.248.9:30303"]|g' /var/lib/bor/config.toml` |
