<!--- Hugo front matter used to generate the website version of this page:
linkTitle: RocketMQ
--->

# Semantic Conventions for RocketMQ

**Status**: [Experimental][DocumentStatus]

The Semantic Conventions for [Apache RocketMQ](https://rocketmq.apache.org/) extend and override the [Messaging Semantic Conventions](README.md)
that describe common messaging operations attributes in addition to the Semantic Conventions
described on this page.

`messaging.system` MUST be set to `"rocketmq"`.

## Apache RocketMQ attributes

Specific attributes for Apache RocketMQ are defined below.

<!-- semconv messaging.rocketmq -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `messaging.rocketmq.namespace` | string | Namespace of RocketMQ resources, resources in different namespaces are individual. | `myNamespace` | Required |
| `messaging.rocketmq.client_group` | string | Name of the RocketMQ producer/consumer group that is handling the message. The client type is identified by the SpanKind. | `myConsumerGroup` | Required |
| `messaging.rocketmq.message.delivery_timestamp` | int | The timestamp in milliseconds that the delay message is expected to be delivered to consumer. | `1665987217045` | Conditionally Required: [1] |
| `messaging.rocketmq.message.delay_time_level` | int | The delay time level for delay message, which determines the message delay time. | `3` | Conditionally Required: [2] |
| `messaging.rocketmq.message.group` | string | It is essential for FIFO message. Messages that belong to the same message group are always processed one by one within the same consumer group. | `myMessageGroup` | Conditionally Required: If the message type is FIFO. |
| `messaging.rocketmq.message.type` | string | Type of message. | `normal` | Recommended |
| `messaging.rocketmq.message.tag` | string | The secondary classifier of message besides topic. | `tagA` | Recommended |
| `messaging.rocketmq.message.keys` | string[] | Key(s) of message, another way to mark message besides message id. | `[keyA, keyB]` | Recommended |
| `messaging.rocketmq.consumption_model` | string | Model of message consumption. This only applies to consumer spans. | `clustering` | Recommended |

**[1]:** If the message type is delay and delay time level is not specified.

**[2]:** If the message type is delay and delivery timestamp is not specified.

`messaging.rocketmq.message.type` MUST be one of the following:

| Value  | Description |
|---|---|
| `normal` | Normal message |
| `fifo` | FIFO message |
| `delay` | Delay message |
| `transaction` | Transaction message |

`messaging.rocketmq.consumption_model` MUST be one of the following:

| Value  | Description |
|---|---|
| `clustering` | Clustering consumption model |
| `broadcasting` | Broadcasting consumption model |
<!-- endsemconv -->

`messaging.client_id` SHOULD be set to the client ID that is automatically generated by the Apache RocketMQ SDK.

[DocumentStatus]: https://github.com/open-telemetry/opentelemetry-specification/blob/v1.21.0/specification/document-status.md