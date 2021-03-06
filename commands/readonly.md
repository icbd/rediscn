---
layout: commands
title: readonly 命令 -- Redis中文资料站
permalink: commands/readonly.html
disqusIdentifier: command_readonly
disqusUrl: http://redis.cn/commands/readonly.html
commandsType: cluster
---

Enables read queries for a connection to a Redis Cluster slave node. 

Normally slave nodes will redirect clients to the authoritative master for
the hash slot involved in a given command, however clients can use slaves
in order to scale reads using the `READONLY` command.

`READONLY` tells a Redis Cluster slave node that the client is willing to
read possibly stale data and is not interested in running write queries.

When the connection is in readonly mode, the cluster will send a redirection
to the client only if the operation involves keys not served by the slave's
master node. This may happen because:

1. The client sent a command about hash slots never served by the master of this slave.
2. The cluster was reconfigured (for example resharded) and the slave is no longer able to serve commands for a given hash slot.

@return

@simple-string-reply
