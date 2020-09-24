Ingest indicator feeds from OpenCTI.
## Configure OpenCTI Feed on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for OpenCTI Feed.
3. Click **Add instance** to create and configure a new integration instance.

| **Parameter** | **Description** | **Required** |
| --- | --- | --- |
| apikey | API Key | True |
| base_url | Base URL | True |
| indicator_types | Indicators Type to fetch | True |
| max_indicator_to_fetch | Max. indicators per fetch \(default is 500\) | False |
| feed | Fetch indicators | False |
| feedReputation | Indicator Reputation | False |
| feedReliability | Source Reliability | True |
| feedExpirationPolicy |  | False |
| feedExpirationInterval |  | False |
| feedFetchInterval | Feed Fetch Interval | False |
| feedTags | Tags | False |
| feedBypassExclusionList | Bypass exclusion list | False |
| insecure | Trust any certificate \(not secure\) | False |
| proxy | Use system proxy settings | False |

####The indicator types parameter
The Possible values that they are supported in XSOAR are:

| **Types** |
| --- |
| ALL |
| User-Account |
| Domain |
| Email-Address| 
| File-md5| 
|File-sha1| |
|File-sha256|
|HostName| 
|IPV4-Addr|
|IPV6-Addr| 
|Registry-Key-Value|
|URL|
 
or another type that they are supported in OpenCTI,
But for that you need to create a Indicator Type on XSOAR with the specific type you want or create or a classification.
they are:

| **Types** |
| --- |
|autonomous-system|
|cryptographic-key|
|cryptocurrency-wallet|
|email-subject|
|directory|
|file-name|
|ile-path|
|mac-addr|
|mutex|
|pdb-path|
|process|
|registry-key-value|
|user-agent|
|windows-service-name|
|windows-service-display-name|
|windows-scheduled-task|
|x509-certificate-issuer|
|x509-certificate-serial-number|


4. Click **Test** to validate the URLs, token, and connection.
## Commands
You can execute these commands from the Demisto CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.
### opencti-get-indicators
***
Gets indicators from the feed.


#### Base Command

`opencti-get-indicators`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| limit | The maximum number of indicators to return per fetch. The default value is "50". | Optional | 
| indicator_types | The indicator types to fetch. Possible values are: "ALL", "User-Account", "Domain", "Email-Address", "File-md5", "File-sha1", "File-sha256", "HostName", "IPV4-Addr", "IPV6-Addr", "Registry-Key-Value", "URL" That they are supported in XSOAR, or another unsupported type, a clear explanation and the list of all types appears in the README. The default is "ALL". | Optional | 
| last_id | The last ID from the previous call from which to begin pagination for this call. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| OpenCTI.Indicators.type | String | Indicator type. | 
| OpenCTI.Indicators.value | String | Indicator value. | 
| OpenCTI.LastRunID | String | the id of the last fetch to use pagination. | 


#### Command Example
```!opencti-get-indicators limit=2 indicator_types=domain```

#### Context Example
```
{
    "OpenCTI": {
        "Indicators": [
            {
                "type": "Domain",
                "value": "test.com"
            },
            {
                "type": "Domain",
                "value": "test1.com"
            }
        ],
        "LastRunID": "YXJyYXljb25uZWN0aW9uOjI="
    }
}
```

#### Human Readable Output

>### Indicators from OpenCTI
>|type|value|
>|---|---|
>| Domain | test.com |
>| Domain | test.com |


### opencti-reset-fetch-indicators
***
WARNING: This command will reset your fetch history.


#### Base Command

`opencti-reset-fetch-indicators`
#### Input

There are no input arguments for this command.

#### Context Output

There is no context output for this command.

#### Command Example
```!opencti-reset-fetch-indicators```

#### Context Example
```
{}
```

#### Human Readable Output

>Fetch history deleted successfully