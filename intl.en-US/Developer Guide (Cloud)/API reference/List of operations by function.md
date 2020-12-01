---
keyword: [Internet of Things, IoT, IoT Platform, cloud, API]
---

# List of operations by function

The following tables describe the API operations that are available for IoT Platform.

## API operations for products

|API|Description|
|:--|:----------|
|[CreateProduct](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/CreateProduct.md)|Creates a product.|
|[UpdateProduct](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/UpdateProduct.md)|Modifies the information of a product.|
|[QueryProductList](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/QueryProductList.md)|Queries products.|
|[QueryProduct](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/QueryProduct.md)|Queries the details of a product.|
|[DeleteProduct](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/DeleteProduct.md)|Deletes a product.|
|[CreateProductTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/CreateProductTags.md)|Creates tags for a product.|
|[UpdateProductTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/UpdateProductTags.md)|Updates the tags of a product.|
|[DeleteProductTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/DeleteProductTags.md)|Deletes the tags of a product.|
|[ListProductTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/ListProductTags.md)|Queries all the tags of a product.|
|[ListProductByTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/ListProductByTags.md)|Queries products by tag.|
|[UpdateProductFilterConfig](/intl.en-US/Developer Guide (Cloud)/API reference/Manage products/UpdateProductFilterConfig.md)|Modifies the deduplication rule for properties that are reported by the devices of a product.|

## API operations for devices

|API|Description|
|:--|:----------|
|[RegisterDevice](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/RegisterDevice.md)|Creats a device.|
|[QueryDeviceDetail](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceDetail.md)|Queries the details of a device.|
|[BatchQueryDeviceDetail](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchQueryDeviceDetail.md)|Queries the details of multiple devices.|
|[QueryDevice](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDevice.md)|Queries the devices of a product.|
|[DeleteDevice](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/DeleteDevice.md)|Deletes a device.|
|[GetDeviceStatus](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/GetDeviceStatus.md)|Queries the status of a device.|
|[BatchGetDeviceState](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchGetDeviceState.md)|Queries the statuses of devices.|
|[DisableThing](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/DisableThing.md)|Disables a device.|
|[EnableThing](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/EnableThing.md)|Enables a device.|
|[ResetThing](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/ResetThing.md)|Resets a device.|
|[BatchCheckDeviceNames](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchCheckDeviceNames.md)|Specifies custom device names. IoT Platform checks whether these device names are valid.|
|[BatchRegisterDeviceWithApplyId](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchRegisterDeviceWithApplyId.md)|Creates multiple devices by application ID.|
|[BatchRegisterDevice](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchRegisterDevice.md)|Creates multiple devices.|
|[QueryBatchRegisterDeviceStatus](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryBatchRegisterDeviceStatus.md)|Queries the statuses of multiple devices.|
|[QueryPageByApplyId](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryPageByApplyId.md)|Queries multiple devices by application ID.|
|[SaveDeviceProp](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/SaveDeviceProp.md)|Creates tags for a device.|
|[QueryDeviceProp](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceProp.md)|Queries the tags of a device.|
|[DeleteDeviceProp](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/DeleteDeviceProp.md)|Deletes the tags of a device.|
|[GetThingTopo](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/GetThingTopo.md)|Queries the topological relationship of a gateway or sub-device.|
|[NotifyAddThingTopo](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/NotifyAddThingTopo.md)|Notifies a gateway to build a topological relationship with devices.|
|[BatchAddTingTopo](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchAddTingTopo.md)|Builds a topological relationship with multiple devices.|
|[RemoveThingTopo](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/RemoveThingTopo.md)|Removes the topological relationships of a device.|
|[QueryDeviceStatistics](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceStatistics.md)|Queries device statistics.|
|[GetGatewayBySubDevice](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/GetGatewayBySubDevice.md)|Queries the information of a gateway based on sub-device information.|
|[QueryDeviceByTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceByTags.md)|Queries devices by tag.|
|[QueryDeviceFileList](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceFileList.md)|Queries the information of all files that are uploaded to IoT Platform from a device.|
|[QueryDeviceFile](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceFile.md)|Queries the information of a file that is uploaded to IoT Platform from a device.|
|[DeleteDeviceFile](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/DeleteDeviceFile.md)|Deletes a file that is uploaded to IoT Platform from a device.|
|[BatchUpdateDeviceNickname](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/BatchUpdateDeviceNickname.md)|Modifies the aliases of multiple devices.|
|[t1847845.md\#](/intl.en-US/Developer Guide (Cloud)/API reference/Manage devices/QueryDeviceByStatus.md)|Queries devices by status.|

## API operations for device groups

|API|Description|
|:--|:----------|
|[CreateDeviceGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/CreateDeviceGroup.md)|Creates a device group.|
|[DeleteDeviceGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/DeleteDeviceGroup.md)|Deletes a device group.|
|[UpdateDeviceGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/UpdateDeviceGroup.md)|Modifies the information of a device group.|
|[QueryDeviceGroupInfo](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QueryDeviceGroupInfo.md)|Queries the details of a device group.|
|[QueryDeviceGroupList](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QueryDeviceGroupList.md)|Queries all device groups.|
|[BatchAddDeviceGroupRelations](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/BatchAddDeviceGroupRelations.md)|Adds devices to a device group.|
|[BatchDeleteDeviceGroupRelations](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/BatchDeleteDeviceGroupRelations.md)|Removes a device from a device group.|
|[SetDeviceGroupTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/SetDeviceGroupTags.md)|Creates tags for or modifies the tags of a device group.|
|[QueryDeviceGroupTagList](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QueryDeviceGroupTagList.md)|Queries the tags of a device group.|
|[QueryDeviceGroupByDevice](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QueryDeviceGroupByDevice.md)|Queries the information of the device group to which a specified device belongs.|
|[QuerySuperDeviceGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QuerySuperDeviceGroup.md)|Queries the information of a parent group by sub-group ID.|
|[QueryDeviceListByDeviceGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QueryDeviceListByDeviceGroup.md)|Queries all devices in a device group.|
|[QueryDeviceGroupByTags](/intl.en-US/Developer Guide (Cloud)/API reference/Manage device groups/QueryDeviceGroupByTags.md)|Queries the information of device groups by tag.|

## API operations for Thing Specification Language \(TSL\) models

|API|Description|
|---|-----------|
|[CreateThingModel](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/CreateThingModel.md)|Adds the features of a product or extended information to a TSL model.|
|[UpdateThingModel](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/UpdateThingModel.md)|Modifies the feature of a product or extended information for a TSL model.|
|[QueryThingModel](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/QueryThingModel.md)|Queries the feature details of a TSL model for a product.|
|[CopyThingModel](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/CopyThingModel.md)|Copies the TSL model of a product to a destination product.|
|[PublishThingModel](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/PublishThingModel.md)|Publishes the TSL model of a product.|
|[t1857517.md\#](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/DeleteThingModel.md)|Removes a feature from a TSL model for a product.|
|[ListThingTemplates](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/ListThingTemplates.md)|Queries all product categories that are predefined in IoT Platform.|
|[GetThingTemplate](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/GetThingTemplate.md)|Queries the standard TSL information of a category.|
|[ListThingModelVersion](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/ListThingModelVersion.md)|Queries the TSL versions of a product.|
|[GetThingModelTsl](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/GetThingModelTsl.md)|Queries the TSL model of a product.|
|[ImportThingModelTsl](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/ImportThingModelTsl.md)|Imports a TSL model for a product. Extended TSL information cannot be imported.|
|[QueryThingModelPublished](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/QueryThingModelPublished.md)|Queries the feature details of a published TSL model for a product.|
|[GetThingModelTslPublished](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/GetThingModelTslPublished.md)|Queries the information of a published TSL model for a product.|
|[QueryThingModelExtendConfig](/intl.en-US/Developer Guide (Cloud)/API reference/Manage TSL models/QueryThingModelExtendConfig.md)|Queries the extended information of a TSL model for a product.|

## API operations for TSL usage

|API|Description|
|:--|:----------|
|[SetDeviceProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDeviceProperty.md)|Sets properties for a device.|
|[SetDevicesProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDevicesProperty.md)|Sets properties for multiple devices.|
|[InvokeThingService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingService.md)|Invokes a service on a device.|
|[InvokeThingsService](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/InvokeThingsService.md)|Invokes a service on multiple devices.|
|[QueryDevicePropertyData](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/QueryDevicePropertyData.md)|Queries the property records of a device.|
|[QueryDevicePropertiesData](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/QueryDevicePropertiesData.md)|Queries the statistics of multiple properties of a device.|
|[QueryDeviceEventData](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/QueryDeviceEventData.md)|Queries the event records of a device.|
|[QueryDeviceServiceData](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/QueryDeviceServiceData.md)|Queries the service records of a device.|
|[SetDeviceDesiredProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/SetDeviceDesiredProperty.md)|Sets expected property values for a device.|
|[QueryDeviceDesiredProperty](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/QueryDeviceDesiredProperty.md)|Queries the expected property values of a device.|
|[QueryDevicePropertyStatus](/intl.en-US/Developer Guide (Cloud)/API reference/Use TSL models/QueryDevicePropertyStatus.md)|Queries the property snapshots of a device.|

## API operations for data forwarding

|API|Description|
|:--|:----------|
|[ListRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/ListRule.md)|Queries rules.|
|[CreateRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/CreateRule.md)|Creates a rule.|
|[GetRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/GetRule.md)|Queries the details of a rule.|
|[UpdateRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/UpdateRule.md)|Modifies a rule.|
|[DeleteRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/DeleteRule.md)|Deletes a rule.|
|[ListRuleActions](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/ListRuleActions.md)|Queries rule actions.|
|[GetRuleAction](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/GetRuleAction.md)|Queries the details of a rule action.|
|[CreateRuleAction](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/CreateRuleAction.md)|Creates a rule action.|
|[UpdateRuleAction](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/UpdateRuleAction.md)|Modifies a rule action.|
|[DeleteRuleAction](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/DeleteRuleAction.md)|Deletes a rule action.|
|[StartRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/StartRule.md)|Enables a rule.|
|[StopRule](/intl.en-US/Developer Guide (Cloud)/API reference/Data forwarding/StopRule.md)|Disables a rule.|

## API operations for topics

|API|Description|
|:--|:----------|
|[QueryProductTopic](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/QueryProductTopic.md)|Queries the topic categories of a product.|
|[CreateProductTopic](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/CreateProductTopic.md)|Creates a topic category for a product.|
|[UpdateProductTopic](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/UpdateProductTopic.md)|Modifies a topic category.|
|[DeleteProductTopic](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/DeleteProductTopic.md)|Deletes a topic category.|
|[CreateTopicRouteTable](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/CreateTopicRouteTable.md)|Creates message routing relationships between topics.|
|[QueryTopicRouteTable](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/QueryTopicRouteTable.md)|Queries the destination topics that subscribe to a source topic.|
|[QueryTopicReverseRouteTable](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/QueryTopicReverseRouteTable.md)|Queries the source topics to which a destination topic subscribes.|
|[DeleteTopicRouteTable](/intl.en-US/Developer Guide (Cloud)/API reference/Manage Topics/DeleteTopicRouteTable.md)|Deletes message routing relationships between topics.|

## API operations for server-side subscriptions

|API|Description|
|:--|:----------|
|[CreateSubscribeRelation](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/CreateSubscribeRelation.md)|Creates a Message Service \(MNS\) or AMQP server-side subscription.|
|[UpdateSubscribeRelation](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/UpdateSubscribeRelation.md)|Modifies an MNS or AMQP server-side subscription.|
|[QuerySubscribeRelation](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/QuerySubscribeRelation.md)|Queries an MNS or AMQP server-side subscription.|
|[DeleteSubscribeRelation](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/DeleteSubscribeRelation.md)|Deletes an MNS or AMQP server-side subscription.|
|[CreateConsumerGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/CreateConsumerGroup.md)|Creates a consumer group that is required for an AMQP server-side subscription.|
|[UpdateConsumerGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/UpdateConsumerGroup.md)|Modifies the name of a consumer group.|
|[QueryConsumerGroupByGroupId](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/QueryConsumerGroupByGroupId.md)|Queries the details of a consumer group by consumer group ID.|
|[QueryConsumerGroupList](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/QueryConsumerGroupList.md)|Queries all the consumer groups of an account, or performs a fuzzy search by consumer group name.|
|[QueryConsumerGroupStatus](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/QueryConsumerGroupStatus.md)|Queries the status of a consumer group when an AMQP server-side subscription is enabled. The status information includes the online client information, message consumption rate, number of accumulated messages, and latest message consumption time.|
|[ResetConsumerGroupPosition](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/ResetConsumerGroupPosition.md)|Clears the accumulated messages of a consumer group when an AMQP server-side subscription is enabled.|
|[DeleteConsumerGroup](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/DeleteConsumerGroup.md)|Deletes a consumer group.|
|[CreateConsumerGroupSubscribeRelation](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/CreateConsumerGroupSubscribeRelation.md)|Adds a consumer group to an AMQP subscription.|
|[DeleteConsumerGroupSubscribeRelation](/intl.en-US/Developer Guide (Cloud)/API reference/Server-side subscription/DeleteConsumerGroupSubscribeRelation.md)|Removes a consumer group from multiple consumer groups of an AMQP subscription.|

## API operations for messaging

|API|Description|
|:--|:----------|
|[Pub](/intl.en-US/Developer Guide (Cloud)/API reference/Communications/Pub.md)|Publishes messages to a topic.|
|[RRpc](/intl.en-US/Developer Guide (Cloud)/API reference/Communications/RRpc.md)|Sends a request to a device and receives a response from the device at the same time.|
|[PubBroadcast](/intl.en-US/Developer Guide (Cloud)/API reference/Communications/PubBroadcast.md)|Broadcasts a message.|

## API operations for device shadows

|API|Description|
|:--|:----------|
|[GetDeviceShadow](/intl.en-US/Developer Guide (Cloud)/API reference/Device shadows/GetDeviceShadow.md)|Queries the shadow information of a device.|
|[UpdateDeviceShadow](/intl.en-US/Developer Guide (Cloud)/API reference/Device shadows/UpdateDeviceShadow.md)|Modifies the shadow information of a device.|

## API operations for OTA updates

|API|Description|
|---|-----------|
|[GenerateOTAUploadURL](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/GenerateOTAUploadURL.md)|Generates the URL and details of an update package to be uploaded to Object Storage Service \(OSS\).|
|[GenerateDeviceNameListURL](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/GenerateDeviceNameListURL.md)|Generates the URL and details of a device list file to be uploaded to OSS. When you create a static update batch, you can specify devices to be updated in a device list file.|
|[CreateOTAFirmware](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CreateOTAFirmware.md)|Creates an update package.|
|[DeleteOTAFirmware](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/DeleteOTAFirmware.md)|Deletes an update package.|
|[ListOTAFirmware](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/ListOTAFirmware.md)|Queries update packages.|
|[QueryOTAFirmware](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/QueryOTAFirmware.md)|Queries the details of an update package.|
|[CreateOTAVerifyJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CreateOTAVerifyJob.md)|Creates a verification task for an update package.|
|[CreateOTAStaticUpgradeJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CreateOTAStaticUpgradeJob.md)|Creates a static update batch.|
|[CreateOTADynamicUpgradeJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CreateOTADynamicUpgradeJob.md)|Creates a dynamic update batch.|
|[ListOTAJobByFirmware](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/ListOTAJobByFirmware.md)|Queries the update batches of an update package.|
|[ListOTAJobByDevice](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/ListOTAJobByDevice.md)|Queries the update batches of an update package by device.|
|[ListOTATaskByJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/ListOTATaskByJob.md)|Queries the update tasks of a device by update batch.|
|[QueryOTAJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/QueryOTAJob.md)|Queries the details of an update task.|
|[CancelOTAStrategyByJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CancelOTAStrategyByJob.md)|Cancels an update policy that is related to a dynamic update task.|
|[CancelOTATaskByDevice](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CancelOTATaskByDevice.md)|Cancels the pending device update tasks of an update package.|
|[CancelOTATaskByJob](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CancelOTATaskByJob.md)|Cancels the device update task of an update batch.|
|[CreateOTAModule](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/CreateOTAModule.md)|Creats an OTA module for a product.|
|[UpdateOTAModule](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/UpdateOTAModule.md)|Modifies the alias of an OTA module.|
|[DeleteOTAModule](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/DeleteOTAModule.md)|Deletes a custom OTA module.|
|[ListOTAModuleByProduct](/intl.en-US/Developer Guide (Cloud)/API reference/OTA update/ListOTAModuleByProduct.md)|Queries the OTA modules of a product.|

