# VIP

A player can be a VIP, it was introduced around patch 5395 [[Reference]](https://cooldown.dev/topic/7-guide-client-patch-notes/) and the level was set by how much real-life money the player had spent on the game.

On client version 5517, there are six levels of VIP where each level subsequently opens up additional features.

## VIP Levels

The features & benefits of each VIP level:

| Feature | Level 1 | Level 2 | Level 3 | Level 4 | Level 5 | Level 6 |
|:---------|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| Remote warehouse (Market, Twin City) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Free flowers per day 🟠 | 2 | 3 | 5 | 10 | 15 | 30 |
| Extra Lottery chances 🟠 | +10 | +20 | +30 | +40 | +50 | +60 |
| Bonus Blessing time 🟠 | +10% | +15% | +20% | +30% | +30% | +30% |
| Max friends 🟠 | 55 | 60 | 70 | 80 | 90 | 100 |
| Offline Training hours 🟠 | 16 | 17 | 18 | 19 | 21 | 24 |
| Refine/Purify time extension 🟠 | +1 day | +2 days | +4 days | +7 days | +7 days | +7 days |
| Free Labyrinth entry 🟠 | every 7d | every 6d | every 5d | every 4d | every 3d | every 2d |
| Remote warehouse (Desert City) | | ✓ | ✓ | ✓ | ✓ | ✓ |
| Remote repair equipped items | | ✓ | ✓ | ✓ | ✓ | ✓ |
| VIP Furniture 🟠 | | ✓ | ✓ | ✓ | ✓ | ✓ |
| City Teleport 🟠 | | ✓ | ✓ | ✓ | ✓ | ✓ |
| Remote warehouse (Ape City) | | | ✓ | ✓ | ✓ | ✓ |
| Remote compose items | | | ✓ | ✓ | ✓ | ✓ |
| Extra Demon Exterminators quest per day | | | ✓ | ✓ | ✓ | ✓ |
| Portal Teleport 🟠🔷 | | | ✓ | ✓ | ✓ | ✓ |
| City Teleport Team 🟠♦️ | | | ✓ | ✓ | ✓ | ✓ |
| Remote warehouse (Bird Island) | | | | ✓ | ✓ | ✓ |
| Keep 50% EXP on PK death | | | | ✓ | ✓ | ✓ |
| VIP Avatars 🟠 | | | | ✓ | ✓ | ✓ |
| VIP Hairstyles 🟠 | | | | ✓ | ✓ | ✓ |
| Frozen Grotto 5F free entries/day 🟠 | | | | 1 | 3 | 5 |
| Extra Study Points quest 🟠 | | | | ✓ | ✓ | ✓ |
| Remote warehouse (Phoenix Castle) | | | | | ✓ | ✓ |
| Remote all warehouses | | | | | | ✓ |
| Portal Teleport Team 🟠🔷♦️ | | | | | | ✓ |

🟠 Sourced from Client 5517 [CN_Res.ini](../files/content/cn_res.ini.md). If not marked, then it is sourced from [Archived Documentation](https://web.archive.org/web/20170703175033/http://vips.99.com/CO/rank.html) 

♦️ If the player is part of a Team, they can invoke a teleport for the whole team. A message is sent to each team member asking to confirm the teleport. The team teleport functionality appears to be handled via [MsgVipUserHandle](../network/messages/msgvipuserhandle.md) (further analysis is required)

🔷 Portal Teleport enables teleporting to specific parts of some maps (Like the Turtledoves Section of WindPlain) These values can be found in the client's [VipTrans.ini](../files/content/viptrans.ini.md) file. It is also referred to as 'SuperSend' in [GUI.ini](../files/content/gui.ini.md)

-------------

### VIP Level in MsgUserInfo

The player's VIP level is first sent to the client when the game server initializes the hero in [MsgUserInfo](../network/messages/msguserinfo.md) as a UInt32. 

The player's VIP level is used in comparisons both server-side & client-side. For example, a level 3 VIP can have up to 70 friends, this is validated both in the client & should be validated server-side when adding a friend.


### VIP Dialog Buttons via MsgVipFunctionValidNotify

The player must be at least VIP Level 1 before the VIP button is shown above the chat bar. The VIP dialog will always show 'RemoteWarehouse', 'RemoteRepair' and 'RemoteCompose'. Remote-Compose is greyed-out and disabled until VIP Level 3. For the other buttons, the server must send a bitwise flag in the packet [MsgVipFunctionValidNotify](../network/messages/msgvipfunctionvalidnotify.md) to the client to determine if the button is visible. The server should send this message during the login sequence while processing [MsgUserInfo](../network/messages/msguserinfo.md).

The values of the bitwise flag can be found in the client's [GUI.ini](../files/content/gui.ini.md) file, with the ini-heading `[338-$BIT_POSITION]`, inside the ini-section would be the VIP Button Function. For example: [338-11] -> `Vip_HairstyleBtn` - shows that the 11th bitflag decides whether or not to show a button in the VIP dialog with hover-over text that the player has access to VIP Hairstyles.

Some buttons perform an action, such as opening the Teleport Team dialog. Some buttons only have hover-over text such as informing how many flowers they can send based on their VIP level and have no action.

The values of the bitwise flag to show or hide a button in the VIP dialog for client 5517 are:

```protobuf
enum VipDialogButtons {
  PORTAL_TELEPORT         = 0x0001; // Button opens a dialog
  VIP_AVATARS             = 0x0002; // Button opens a dialog
  EXTRA_FLOWERS           = 0x0004; // Hover-over button text only
  FROZEN_GROTTO_5F        = 0x0008; // Hover-over button text only
  PORTAL_TELEPORT_TEAM    = 0x0010; // Button opens a dialog
  CITY_TELEPORT           = 0x0020; // Button opens a dialog
  CITY_TELEPORT_TEAM      = 0x0040; // Button opens a dialog
  EXTRA_BLESSING_TIME     = 0x0080; // Hover-over button text only
  OFFLINE_TRAINING_HOURS  = 0x0100; // Hover-over button text only
  REFINE_PURIFY_EXTENSION = 0x0200; // Hover-over button text only
  ADDITIONAL_FRIEND_SLOTS = 0x0400; // Hover-over button text only
  VIP_HAIRSTYLES          = 0x0800; // Hover-over button text only
  FREE_LABYRINTH_ACCESS   = 0x1000; // Hover-over button text only
  MORE_DAILY_QUESTS       = 0x2000; // Hover-over button text only
  VIP_FURNITURE           = 0x4000; // Hover-over button text only
  MORE_LOTTERY_CHANCES    = 0x8000; // Hover-over button text only
}
```

Therefore, the bitflag values for each VIP Level that the server must send via [MsgVipFunctionValidNotify](../network/messages/msgvipfunctionvalidnotify.md) are:

```protobuf
enum VipLevel {
  VIP_LEVEL_1 = 0x9784;
  VIP_LEVEL_2 = 0xD7A4;
  VIP_LEVEL_3 = 0xD7E5;
  VIP_LEVEL_4 = 0xFFEF;
  VIP_LEVEL_5 = 0xFFEF;
  VIP_LEVEL_6 = 0xFFFF;
}
```