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

**The following details are passed to the GithubApi:**
   * if _ghArtifactType_ is 'Repo':  _ghArtifactId_ is passed, it contains the repository id.
   * if _ghArtifactType_is 'Account': _ghArtifactId_ is passed, it contains the user id.


if the authorization is successfull, using the GithubAPI We will get the details about each subscription.

Results are displayed as hyperlinks. Text will be the full_name of the repository or the github account name. The hyperlinks will redirect to the repository or the github user account.

If the user is not signed in, the card will be the showing the message ***Not subscribe to any repositories or accounts.***

