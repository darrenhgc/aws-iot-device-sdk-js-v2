# AWS IoT SDK for Javascript v2

Next generation AWS IoT Client SDK for Javascript.

This project is in **GENERAL AVAILABILITY**. If you have any issues or feature requests,
please file an issue or pull request.

This SDK is built on the AWS Common Runtime, a collection of libraries
([1](https://github.com/awslabs/aws-c-common),
[2](https://github.com/awslabs/aws-c-io),
[3](https://github.com/awslabs/aws-c-mqtt),
[4](https://github.com/awslabs/aws-c-http),
[5](https://github.com/awslabs/aws-c-cal) ...) written in C to be
cross-platform, high-performance, secure, and reliable. The libraries are bound
to JS by the [awscrt](https://github.com/awslabs/aws-crt-nodejs) package.

The aws-crt package can be installed via npm 
```
npm install aws-crt
```

Integration with AWS IoT Services such as
[Device Shadow](https://docs.aws.amazon.com/iot/latest/developerguide/iot-device-shadows.html)
and [Jobs](https://docs.aws.amazon.com/iot/latest/developerguide/iot-jobs.html)
is provided by code that been generated from a model of the service.

# Installation
## Minimum Requirements
*   Node 10.x+

## Install from npm
```
npm install aws-iot-device-sdk-v2
```

## Build from source
```
npm install
```

# Samples

## node/pub_sub
This sample uses the
[Message Broker](https://docs.aws.amazon.com/iot/latest/developerguide/iot-message-broker.html)
for AWS IoT to send and receive messages
through an MQTT connection. On startup, the device connects to the server,
subscribes to a topic, and begins publishing messages to that topic.
The device should receive those same messages back from the message broker,
since it is subscribed to that same topic.
Status updates are continually printed to the console.

Source: `samples/node/pub_sub`

Run the sample like this:
```
npm install
node dist/index.js --endpoint <endpoint> --root-ca <file> --cert <file> --key <file>
```

Your Thing's
[Policy](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html)
must provide privileges for this sample to connect, subscribe, publish,
and receive.
<details>
<summary>(see sample policy)</summary>
<pre>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:Publish",
        "iot:Receive"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topic/samples/test"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Subscribe"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:topicfilter/samples/test"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iot:Connect"
      ],
      "Resource": [
        "arn:aws:iot:<b>region</b>:<b>account</b>:client/samples-client-id"
      ]
    }
  ]
}
</pre>
</details>

## node/basic_discovery

This sample intended for use directly with the 
[Getting Started with AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/latest/developerguide/gg-gs.html) guide.

# License

This library is licensed under the Apache 2.0 License.
