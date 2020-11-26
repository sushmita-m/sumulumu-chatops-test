## Database
_Tables_: chatopssubscriptions, chatopsInstallations
# List of workflows:
## subscribe
## unsubscribe
## subscribe list
Lists the repositories and accounts that users have subscribed to in the given channel.

_command_: `@github subscribe list`

_prerequisites:_
Users should be signed in on the Github app on Teams to view the list of subscriptions.

## Decision:
***Request:***
We pass in the _channelId_, _teamId_, _clientAppId_ from the context. We are querying the **chatopssubscriptions** table with these id's. 

***Reply:***
We get the _ghInstallationId_ from **chatopsinstallations** table (_chatOpsInstallationId_ is a foreign key in the **chatopssubscriptions** table).

We get the _ghArtifactId_, _ghArtifactType_ from the chatopssubscriptions table.

_ghInstallationId_ is used to get authorization to the github client which will be used to make the api calls to get details about the artifact (This will tell us if the app has been uninstalled from the repo/account after the subscription)

