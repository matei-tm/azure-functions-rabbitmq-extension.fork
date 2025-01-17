|Branch|Status|
|---|---|
|dev|[![Build Status](https://azfunc.visualstudio.com/Azure%20Functions/_apis/build/status/Azure.azure-functions-rabbitmq-extension?branchName=dev)](https://azfunc.visualstudio.com/Azure%20Functions/_build/latest?definitionId=48&branchName=dev)|

# RabbitMQ Binding Support for Azure Functions
NuGet Package [Microsoft.Azure.WebJobs.Extensions.RabbitMQ](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.RabbitMQ)

Please note that the RabbitMQ extension is fully supported on Premium and Dedicated plans. Consumption is not supported. The Azure Functions RabbitMQ Binding extensions allow you to send and receive messages using the RabbitMQ API but by writing Functions code. The RabbitMQ output binding sends messages to a specific queue. The RabbitMQ trigger fires when it receives a message from a specific queue.

[RabbitMQ Documentation for the .NET Client](https://www.rabbitmq.com/dotnet-api-guide.html)

To get started with developing with this extension, make sure you first [set up a RabbitMQ endpoint](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Setting-up-a-RabbitMQ-Endpoint). Then you can go ahead and begin developing your functions in [C#](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Samples-in-C%23), [C# Script](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Samples-in-CSX), [JavaScript](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Samples-in-JavaScript), [Python](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Samples-in-Python) or [Java](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Samples-in-Java).

# Samples

See the repository [wiki](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki) for more detailed samples of bindings to different types.

```C#
public static void RabbitMQTrigger_RabbitMQOutput(
    [RabbitMQTrigger("queue", ConnectionStringSetting = "RabbitMQConnectionAppSetting")] string inputMessage,
    [RabbitMQ(
        ConnectionStringSetting = "RabbitMQConnectionAppSetting",
        QueueName = "hello")] out string outputMessage,
    ILogger logger)
{
    outputMessage = inputMessage;
    logger.LogInformation($"RabbitMQ output binding function sent message: {outputMessage}");
}
```

The above sample waits on a trigger from the queue named "queue" connected to the connection string value of key "RabbitMQConnectionAppSetting." The output binding takes the messages from the trigger queue and outputs them to queue "hello" connected to the connection configured by the key "RabbitMQConnectionAppSetting". When running locally, add the connection string setting to local.settings.json file. When running in Azure, add this setting as [Application Setting](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings) for your app.


## Properties

|Property Name|Description|Example|
|--|--|--|
|ConnectionStringSetting|The connection string for the RabbitMQ queue|`amqp://user:password@url:port`|
|QueueName|The name of the source or destination queue.|
|HostName|(ignored if using ConnectionStringSetting) Hostname of the queue|`10.26.45.210`|
|UserName|(ignored if using ConnectionStringSetting) User name to access queue|`user`|
|Password|(ignored if using ConnectionStringSetting) Password to access queue|`password`|
|EnableSsl|Bool to enable or disable SSL in AMQP connection (default false)|`true`|
|SkipCertificateValidation|Bool to enable or disable checking certificate when EnableSsl=true. It will accept RemoteCertificateChainErrors and RemoteCertificateNameMismatch errors (default false. Not recommended for production)|`true`|

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
