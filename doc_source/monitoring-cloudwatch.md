# Monitor Amazon GameLift with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor Amazon GameLift using Amazon CloudWatch, an AWS service that collects raw data and processes it into readable, near real\-time metrics\. These statistics are kept for 15 months, so that you can access historical information and gain a better perspective on how your game server hosting with Amazon GameLift is performing\. You can also set alarms that watch for certain thresholds and send notifications or take actions when those thresholds are met\. For more information, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\.

To access CloudWatch metrics for your games, you can use the AWS Management Console, the AWS CLI, or the CloudWatch API\. The following tables list the metrics and dimensions for Amazon GameLift\. All metrics that are available in CloudWatch are also available in the Amazon GameLift console, which provides the data as a set of customizable graphs\. 

## Amazon GameLift Metrics for Fleets<a name="gamelift-metrics-fleet"></a>

The `AWS/GameLift` namespace includes the following metrics related to activity across a fleet or a group of fleets\. The Amazon GameLift service sends metrics to CloudWatch every minute\. 

### Instances<a name="gamelift-metrics-fleet-instances"></a>


| Metric | Description | 
| --- | --- | 
| `ActiveInstances` |  Instances with ACTIVE status, which means they are running active server processes\. The count includes idle instances and those that are hosting one or more game sessions\. This metric measures current total instance capacity\. This metric can be used with automatic scaling\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `DesiredInstances` |  Target number of active instances that Amazon GameLift is working to maintain in the fleet\. With automatic scaling, this value is determined based on the scaling policies currently in force\. Without automatic scaling, this value is set manually\. This metric is not available when viewing data for fleet metric groups\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `IdleInstances` |  Active instances that are currently hosting zero \(0\) game sessions\. This metric measures capacity that is available but unused\. This metric can be used with automatic scaling\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `MaxInstances` |  Maximum number of instances that are allowed for the fleet\. A fleet's instance maximum determines the capacity ceiling during manual or automatic scaling up\. This metric is not available when viewing data for fleet metric groups\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `MinInstances` |  Minimum number of instances allowed for the fleet\. A fleet's instance minimum determines the capacity floor during manual or automatic scaling down\. This metric is not available when viewing data for fleet metric groups\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PercentIdleInstances` |  Percentage of all active instances that are idle \(calculated as `IdleInstances / ActiveInstances`\)\. This metric can be used for automatic scaling\. Units: Percent Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `InstanceInterruptions` |  Number of spot instances that have been interrupted\. Units: Count Relevant CloudWatch statistics: Sum, Average, Minimum, Maximum | 

### Server Processes<a name="gamelift-metrics-fleet-processes"></a>


| Metric | Description | 
| --- | --- | 
| `ActiveServerProcesses` |  Server processes with ACTIVE status, which means they are running and able to host game sessions\. The count includes idle server processes and those that are hosting game sessions\. This metric measures current total server process capacity\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `HealthyServerProcesses` |  Active server processes that are reporting healthy\. This metric is useful for tracking the overall health of the fleet's game servers\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
|  `PercentHealthyServerProcesses`  |  Percentage of all active server processes that are reporting healthy \(calculated as `HealthyServerProcesses / ActiveServerProcesses`\)\. Units: Percent Relevant CloudWatch statistics: Average, Minimum, Maximum  | 
| `ServerProcessAbnormalTerminations` |  Server processes that were shut down due to abnormal circumstances since the last report\. This metric includes terminations that were initiated by the Amazon GameLift service\. This occurs when a server process stops responding, consistently reports failed health checks, or does not terminate cleanly \(by calling [ ProcessEnding\(\)](https://docs.aws.amazon.com/gamelift/latest/developerguide/integration-server-sdk-cpp-ref-actions.html#integration-server-sdk-cpp-ref-processending)\)\. Units: Count Relevant CloudWatch statistics: Sum, Average, Minimum, Maximum | 
| `ServerProcessActivations` |  Server processes that successfully transitioned from ACTIVATING to ACTIVE status since the last report\. Server processes cannot host game sessions until they are active\. Units: Count Relevant CloudWatch statistics: Sum, Average, Minimum, Maximum | 
| `ServerProcessTerminations` |  Server processes that were shut down since the last report\. This includes all server processes that transitioned to TERMINATED status for any reason, including normal and abnormal process terminations\. Units: Count Relevant CloudWatch statistics: Sum, Average, Minimum, Maximum | 

### Game Sessions<a name="gamelift-metrics-fleet-games"></a>


| Metric | Description | 
| --- | --- | 
| `ActivatingGameSessions` |  Game sessions with ACTIVATING status, which means they are in the process of starting up\. Game sessions cannot host players until they are active\. High numbers for a sustained period of time may indicate that game sessions are not transitioning from ACTIVATING to ACTIVE status\. This metric can be used with automatic scaling\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `ActiveGameSessions` |  Game sessions with ACTIVE status, which means they are able to host players, and are hosting zero or more players\. This metric measures the total number of game sessions currently being hosted\. This metric can be used with automatic scaling\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `AvailableGameSessions` |  Game session slots on active, healthy server processes that are not currently being used\. This metric measures the number of new game sessions that could be started immediately\. This metric can be used with automatic scaling\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PercentAvailableGameSessions` |  Percentage of game session slots on all active server processes \(healthy or unhealthy\) that are not currently being used \(calculated as `AvailableGameSessions / [ActiveGameSessions + AvailableGameSessions + unhealthy server processes]`\)\. This metric can be used with automatic scaling\. Units: Percent Relevant CloudWatch statistics: Average | 
| `GameSessionInterruptions` |  Number of game sessions on spot instances that have been interrupted\. Units: Count Relevant CloudWatch statistics: Sum, Average, Minimum, Maximum | 

### Player Sessions<a name="gamelift-metrics-fleet-players"></a>


| Metric | Description | 
| --- | --- | 
| `CurrentPlayerSessions` |  Player sessions with either ACTIVE status \(player is connected to an active game session\) or RESERVED status \(player has been given a slot in a game session but hasn't yet connected\)\. This metric can be used with automatic scaling\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PlayerSessionActivations` |  Player sessions that transitioned from RESERVED status to ACTIVE since the last report\. This occurs when a player successfully connects to an active game session\. Units: Count Relevant CloudWatch statistics: Sum, Average, Minimum, Maximum | 

## Amazon GameLift Metrics for Queues<a name="gamelift-metrics-queue"></a>

The `GameLift` namespace includes the following metrics related to activity across a game session placement queue\. The Amazon GameLift service sends metrics to CloudWatch every minute\.


| Metric | Description | 
| --- | --- | 
| `AverageWaitTime` | Average amount of time that game session placement requests in the queue with status PENDING have been waiting to be fulfilled\. Units: Seconds Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PlacementsCanceled` |  Game session placement requests that were canceled before timing out since the last report\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PlacementsStarted` |  New game session placement requests that were added to the queue since the last report\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PlacementsSucceeded` | Game session placement requests that resulted in a new game session since the last report\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `PlacementsTimedOut` |  Game session placement requests that reached the queue's timeout limit without being fulfilled since the last report\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `QueueDepth` | Number of game session placement requests in the queue with status PENDING\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 

## Amazon GameLift Metrics for Matchmaking<a name="gamelift-metrics-match"></a>

The `GameLift` namespace includes the following metrics related to matchmaking activity\. The Amazon GameLift service sends metrics to CloudWatch every minute\.

For more information on the sequence of matchmaking activity, see [How Amazon GameLift FlexMatch Works](https://docs.aws.amazon.com/gamelift/latest/developerguide/gamelift-match-howitworks.html)\.


| Metric | Description | 
| --- | --- | 
| `CurrentTickets` | Matchmaking requests currently being processed or waiting to be processed\. Units: Count Relevant CloudWatch statistics: Average, Minimum, Maximum | 
| `MatchAcceptancesTimedOut` | For matchmaking configurations that require acceptance, the potential matches that timed out during acceptance since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `MatchesAccepted` | For matchmaking configurations that require acceptance, the potential matches that were accepted since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `MatchesCreated` | Potential matches that were created since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `MatchesPlaced` | Matches that were successfully placed into a game session since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `MatchesRejected` | For matchmaking configurations that require acceptance, the potential matches that were rejected by at least one player since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `PlayersStarted` | Players in matchmaking tickets that were added since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `RuleEvaluationsPassed` | Rule evaluations during the matchmaking process that passed since the last report\. This metric is limited to the top 50 rules\.Units: CountRelevant CloudWatch statistics: Sum | 
| `RuleEvaluationsFailed` | Rule evaluations during matchmaking that failed since the last report\. This metric is limited to the top 50 rules\. Units: Count Relevant CloudWatch statistics: Sum | 
| `TicketsFailed` |  Matchmaking requests that resulted in failure since the last report\.  Units: Count Relevant CloudWatch statistics: Sum  | 
| `TicketsStarted` |  New matchmaking requests that were created since the last report\. Units: Count Relevant CloudWatch statistics: Sum  | 
| `TicketsTimedOut` | Matchmaking requests that reached the timeout limit since the last report\. Units: Count Relevant CloudWatch statistics: Sum | 
| `TimeToMatch` | For matchmaking requests that were put into a potential match before the last report, the amount of time between ticket creation and potential match creation\. Units: Seconds Relevant CloudWatch statistics: Data Samples, Average, Minimum, Maximum, p99 | 
| `TimeToTicketCancel` |  For matchmaking requests that were canceled before the last report, the amount of time between ticket creation and cancellation\. Units: Seconds Relevant CloudWatch statistics: Data Samples, Average, Minimum, Maximum, p99 | 
| `TimeToTicketSuccess` | For matchmaking requests that succeeded before the last report, the amount of time between ticket creation and successful match placement\. Units: Seconds Relevant CloudWatch statistics: Data Samples, Average, Minimum, Maximum, p99 | 

## Dimensions for Amazon GameLift Metrics<a name="billing-metricdimensions-fleet"></a>

Amazon GameLift supports filtering metrics by the following dimensions\.


| Dimension | Description | 
| --- | --- | 
|  `FleetId`  |  Unique identifier for a single fleet\. This dimension is used with all metrics for instances, server processes, game sessions, and player sessions\. It is not used with metrics for queues and matchmaking\.  | 
|  `FleetMetricsGroup`  |  Unique identifier for a collection of fleets\. A fleet is included in a fleet metric group by adding the metric group name to the fleet's attributes \(see [UpdateFleetAttributes\(\)](https://docs.aws.amazon.com/gamelift/latest/apireference/API_UpdateFleetAttributes.html)\)\. This dimension is used with all metrics for instances, server processes, game sessions, and player sessions\. It is not used with metrics for queues and matchmaking\.  | 
|  `QueueName`  |  Unique identifier for a single queue\. This dimension is used with metrics for game session placement queues only\.   | 
|  `MatchmakingConfigurationName`  |  Unique identifier for a single matchmaking configuration\. This dimension is used with metrics for matchmaking only\.   | 
|  `MatchmakingConfigurationName-RuleName`  |  Unique identifier for the intersect of a matchmaking configuration and a matchmaking rule\. This dimension is used with metrics for matchmaking only\.   | 
|  `InstanceType`  |  Unique identifier for an EC2 instance type designation, such as "C4\.large"\. This dimension is used with metrics for spot instances only\.   | 
|  `OperatingSystem`  |  Unique identifier for the operating system of an instance\. This dimension is used with metrics for spot instances only\.   | 