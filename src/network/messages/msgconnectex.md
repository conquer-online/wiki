# MsgConnectEx

This account server message is sent to the client to provide connection details for the selected game server. If authentication failed on the account server, then this message will contain a rejection code and message. In older versions of the client, the rejection message is in Chinese but not actually used by the client besides for validation. It was later removed.

The client also validates the IP address and will reject localhost (127.x.x.x). The game server IP address can be a local (10.x.x.x or 192.x.x.x) or public IP address.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)
* [Patch 5517](#patch-5517)

## Patch 4267

#### Accept Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 32 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1055 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | [Encryption key](/security/tq.md) generator parameter | 6351601 |
| 12 | Char[16] | Info | Game server's IP address | 192.168.1.2 |
| 28 | UInt32 | Port | Game server's port | 5816 |

#### Reject Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1055 |
| 8  | UInt32 | Data | [Rejection type](#rejection-type) | 10 |
| 12 | Char[16] | Info | [Rejection message](#rejection-type) in GB2312 encoding | 帐号名或口令错 |

#### Rejection Type

☑️ Assumed (Observed) - Comet

| Type | Chinese | English |
|:-----|:--------|:--------|
| 1   | 帐号名或口令错 | Invalid account name or password. |
| 10  | 服务器未启动 | The server is down! |
| 11  | 请稍后重新登录 | Please re-login later. |
| 12  | 该帐号被封号 | This account is banned. |
| 999 | 数据库错误 | Unknown Error |

## Patch 5017

#### Accept Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 32 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1055 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | [Encryption key](/security/tq.md) generator parameter | 6351601 |
| 12 | Char[16] | Info | Game server's IP address | 192.168.1.2 |
| 28 | UInt32 | Port | Game server's port | 5816 |

#### Reject Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1055 |
| 8  | UInt32 | Data | [Rejection type](#rejection-type-1) | 10 |

#### Rejection Type

☑️ Assumed (Observed) - Comet

| Type | Description |
|:-----|:--------|
| 1   | Invalid account name or password |
| 10  | Server down |
| 11  | Try again later |
| 12  | Account banned |
| 20  | Server busy |
| 22  | Account locked |
| 30  | Account not activated | 
| 31  | Account activation failed |
| 42  | Server timed out |
| 51  | Max login attempts |
| 70  | Server locked |
| 73  | Old protocol |
| 999 | Unknown error |

## Patch 5517

#### Accept Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 52 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1055 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | [Encryption key](/security/tq.md) generator parameter | 6351601 |
| 12 | UInt32 | Port | Game server's port | 5816 |
| 20 | Char[32] | Info | Game server's IP address | 192.168.1.2 |

#### Reject Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1055 |
| 8  | UInt32 | Data | [Rejection type](#rejection-type-2) | 10 |

#### Rejection Type

✅ Verified (Client)

The following mapping is copied from [Cn_Res.ini](/files/content/cn_res.ini.md).

```
000=Changing Map
001=Invalid Account ID or Password
006=Point Card Expired
007=Monthly Card Expired
010=Server maintenance. Please try again later!
011=Please try again later.
012=This account has been banned.
013=Net cafe mode. Invalid Account ID or Password.
014=Net cafe mode. No more accounts can be logged, at this time.
020=Server is busy.
021=Server is busy. Please try again, later.
022=Your account has been locked. Please contact GM for more help.
024=This account has been banned.
025=This account has been banned.
026=This account has been banned.
027=This account has been banned.
028=This account has been banned.
030=This account has not been activated.
031=Failed to activate the account.
040=Invalid Input
041=Invalid Info
042=Timed Out
043=Please recheck the serial number or retrieve a new one.
044=Invalid Sub-password
045=Please input Sub-password.
046=Unbound
050=Non-cooperator Account
051=Sorry, but you have used up your login attempts. Please wait 30 minutes and try again.
052=Failed to login
053=The same server
054=Database Error
055=Failed to connect to the database.
056=Failed to connect
057=Invalid Account ID
058=Validation timed out.
059=Servers are not configured correctly.
060=Passpod Server Disconnected
061=Failed to process Passpod return
062=Passpod Password Expired
063=Passpod Verification Failed
064=Passpod Certification Expired
065=Passpod Certification Disabled
066=Failed to find the user.
067=Passpod Server Error
068=Passpod has not been input.
070=Server Locked
071=Login has been restricted. Please check the login limit, and try again.
072=Account Locked by Phone
073=Authentication Protocol is invalid or expired.
501=The account has not been bound to any phone
502=The key is wrong. Please rebind it.
504=The sub-key is wrong.
506=Please input the sub-key.
507=Failed to call.
508=Failed to login QQ account
999=Database Error
```