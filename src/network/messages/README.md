# Messages

This subsection organizes messages by the name found in the assembly of the macOS game client. See the table before for a mapping from message type to message definition.

### Message Header

The table below defines TQ's message header. The header is written to all messages first and contains the size of the message (aka. the message length minus the size of the footer) and the message type (a constant identifier for handling the message on the client and server).

| Pos | Type | Description | Example |
|:-------|:-----|:------------|:--------|
| 0 | UInt16 | Message Size | 60 |
| 2 | UInt16 | Message Type | 1001 |

### Message Footer

The message footer in Conquer Online was added in patch 5018. The footer contains an 8-byte string identifying the sender of the message. If the client sent the message, the footer would be "TQClient"; else, it would be "TQServer".

### Message Types

The table below is an abstract and directory of message types used in various patches of Conquer Online.

| Type | Name | Abstract |
|:-----|:-----|:---------|
| 1001 | [MsgRegister](msgregister.md) | New character creation |
| 1004 | [MsgTalk](msgtalk.md) | Game chat and system messages to clients |
| 1005 | [MsgWalk](msgwalk.md) | Role movement on the ground |
| 1006 | [MsgUserInfo](msguserinfo.md) | Character information on login |
| 1008 | [MsgItemInfo](msgiteminfo.md) | Details on an player owned item |
| 1009 | [MsgItem](msgitem.md) | Request to use an item |
| 1010 | [MsgAction](msgaction.md) | General action for a player or entity |
| 1012 | [MsgTick](msgtick.md) | Round-trip tick validation |
| 1014 | [MsgPlayer](msgplayer.md) | Spawn a player or entity |
| 1015 | [MsgName](msgname.md) | Client string update request  |
| 1016 | [MsgWeather](msgweather.md) | Set weather on the game map |
| 1017 | [MsgUserAttrib](msguserattrib.md) | Set user attributes for client |
| 1019 | [MsgFriend](msgfriend.md) | Manages friend and enemy lists |
| 1022 | [MsgInteract](msginteract.md) | Interact or attack player or entity |
| 1023 | [MsgTeam](msgteam.md) | Manages a team of players |
| 1024 | [MsgAllot](msgallot.md) | Allot attribute points |
| 1025 | [MsgWeaponSkill](msgweaponskill.md) | Weapon proficiency update |
| 1026 | [MsgTeamMember](msgteammember.md) | Details on multiple teammates |
| 1027 | [MsgGemEmbed](msggemembed.md) | Embed gem in an item |
| 1028 | [MsgFuse](msgfuse.md) | Fuse material to an item |
| 1029 | [MsgTeamAward](msgteamaward.md) | |
| 1032 | [MsgBattleEffectiveness](msgbattleeffectiveness.md) |  |
| 1033 | [MsgData](msgdata.md) | General integer data message |
| 1034 | [MsgDetainItemInfo](msgdetainiteminfo.md) | Details on a detailed item |
| 1036 | [MsgGodExp](msggodexp.md) | |
| 1037 | [MsgPing](msgping.md) |  |
| 1038 | [MsgSolidify](msgsolidify.md) |  |
| 1039 | [MsgNpcPath](msgnpcpath.md) |  |
| 1040 | [MsgPlayerAttribInfo](msgplayerattribinfo.md) | Player's battle statistics |
| 1041 | [MsgEnemyList](msgenemylist.md) |  |
| 1042 | [MsgMonsterTransform](msgmonstertransform.md) |  |
| 1043 | [MsgTeamRoll](msgteamroll.md) |  |
| 1044 | [MsgLoadMap](msgloadmap.md) |  |
| 1045 | [MsgMailOperation](msgmailoperation.md) |  |
| 1046 | [MsgMailList](msgmaillist.md) |  |
| 1047 | [MsgMailNotify](msgmailnotify.md) |  |
| 1048 | [MsgMailContent](msgmailcontent.md) |  |
| 1049 | [MsgPCServerConfig](msgpcserverconfig.md) |  |
| 1051 | [MsgAccount](msgaccount.md) | Login authentication request |
| 1052 | [MsgConnect](msgconnect.md) | Game server authorization request |
| 1055 | [MsgConnectEx](msgconnectex.md) | Game server connect info  |
| 1056 | [MsgTrade](msgtrade.md) | Trade items and money with a player |
| 1057 | [MsgConnectWithBgp](msgconnectwithbgp.md) |  |
| 1058 | [MsgSynpOffer](msgsynpoffer.md) | Syndicate donation |
| 1059 | [MsgEncryptCode](msgencryptcode.md) | Generated RC5 seed |
| 1060 | [MsgAccount](msgaccount.md) | Login authentication request |
| 1061 | [MsgDutyMinContri](msgdutymincontri.md) |  |
| 1062 | [MsgSynCompete](msgsyncompete.md) |  |
| 1063 | [MsgSelfSynMemAwardRank](msgselfsynmemawardrank.md) |  |
| 1064 | [MsgSponsor](msgsponsor.md) |  |
| 1065 | [MsgSponsorInfo](msgsponsorinfo.md) |  |
| 1066 | [MsgMeteSpecial](msgmetespecial.md) |  |
| 1067 | [MsgLoginNotice](msgloginnotice.md) |  |
| 1070 | [MsgHangUp](msghangup.md) |  |
| 1071 | [MsgCompleteRank](msgcompleterank.md) |  |
| 1072 | [MsgCampFight](msgcampfight.md) |  |
| 1073 | [MsgCampFightInfo](msgcampfightinfo.md) |  |
| 1074 | [MsgPicKeyError](msgpickeyerror.md) |  |
| 1075 | [MsgPicKey](msgpickey.md) |  |
| 1081 | [MsgCheatingProgram](msgcheatingprogram.md) |  |
| 1083 | [MsgRequestKeyLogin](msgrequestkeylogin.md) |  |
| 1084 | [MsgConfirmKeyLogin](msgconfirmkeylogin.md) |  |
| 1086 | [MsgAccount](msgaccount.md) | Login authentication request |
| 1090 | [MsgLoginAccountEx](msgloginaccountex.md) |  |
| 1098 | [MsgConfirmKeyLoginMobile](msgconfirmkeyloginmobile.md) |  |
| 1100 | [MsgPCNum](msgpcnum.md) | Mac address of the client |
| 1101 | [MsgMapItem](msgmapitem.md) | Dropped item on the map floor |
| 1102 | [MsgAccountSoftKb](msgaccountsoftkb.md) |  |
| 1102 | [MsgPackage](msgpackage.md) | Item storage / warehouses |
| 1103 | [MsgMagicInfo](msgmagicinfo.md) | Magic spell the player can cast |
| 1104 | [MsgFlushExp](msgflushexp.md) | Magic spell or skill experience update |
| 1105 | [MsgMagicEffect](msgmagiceffect.md) | Cast a magical attack or effect |
| 1106 | [MsgSyndicateAttributeInfo](msgsyndicateattributeinfo.md) | Guild and guild member details |
| 1107 | [MsgSyndicate](msgsyndicate.md) | Guild action request |
| 1108 | [MsgItemInfoEx](msgiteminfoex.md) | Item details extended for a feature |
| 1109 | [MsgNpcInfoEx](msgnpcinfoex.md) | NPC spawn with health |
| 1110 | [MsgMapInfo](msgmapinfo.md) | Map type flags |
| 1111 | [MsgMessageBoard](msgmessageboard.md) | Categorized message board |
| 1112 | [MsgSynMemberInfo](msgsynmemberinfo.md) |  |
| 1113 | [MsgDice](msgdice.md) | Dice game messages |
| 1114 | [MsgSyncAction](msgsyncaction.md) | Two-player synchronized actions |
| 1115 | [MsgDisconnect](msgdisconnect.md) |  |
| 1121 | [MsgFacebookAccount](msgfacebookaccount.md) |  |
| 1124 | [MsgAccountSRP6](msgaccountsrp6.md) | Requests SRP6 password exchange |
| 1125 | [MsgAccountKalydo](msgaccountkalydo.md) |  |
| 1126 | [MsgInviteTrans](msginvitetrans.md) |  |
| 1127 | [MsgMentorPlayer](msgmentorplayer.md) |  |
| 1128 | [MsgVipUserHandle](msgvipuserhandle.md) |  |
| 1129 | [MsgVipFunctionValidNotify](msgvipfunctionvalidnotify.md) |  |
| 1130 | [MsgTitle](msgtitle.md) | List or change player title |
| 1134 | [MsgTaskStatus](msgtaskstatus.md) |  |
| 1135 | [MsgTaskDetailInfo](msgtaskdetailinfo.md) |  |
| 1136 | [MsgAchievement](msgachievement.md) |  |
| 1150 | [MsgFlower](msgflower.md) |  |
| 1151 | [MsgRank](msgrank.md) |  |
| 1202 | [MsgRegisterFaceBook](msgregisterfacebook.md) |  |
| 1203 | [MsgConnectFaceBook](msgconnectfacebook.md) |  |
| 1213 | [MsgLoginChallengeS](msgloginchallenges.md) | Sends SRP6 challenge |
| 1214 | [MsgLoginProofC](msgloginproofc.md) | Reply for SRP6 challenge |
| 1312 | [MsgFamily](msgfamily.md) | Clan action request |
| 1313 | [MsgFamilyOccupy](msgfamilyoccupy.md) |  |
| 1314 | [MsgLottery](msglottery.md) |  |
| 1315 | [MsgOperatingAct](msgoperatingact.md) |  |
| 1316 | [MsgOperatingActInfo](msgoperatingactinfo.md) |  |
| 1320 | [MsgAuction](msgauction.md) |  |
| 1321 | [MsgAuctionItem](msgauctionitem.md) |  |
| 1322 | [MsgAuctionQuery](msgauctionquery.md) |  |
| 1323 | [MsgPromotionAct](msgpromotionact.md) |  |
| 1324 | [MsgPromotionInfo](msgpromotioninfo.md) |  |
| 1350 | [MsgGameServerShutDown](msggameservershutdown.md) | Shutdown notification |
| 1351 | [MsgSlotAction](msgslotaction.md) |  |
| 1352 | [MsgSlotResult](msgslotresult.md) |  |
| 1518 | [MsgConnectLegalitySpec](msgconnectlegalityspec.md) |  |
| 1542 | [MsgAccountSRP6Ex](msgaccountsrp6ex.md) | Requests SRP6 password exchange |
| 1636 | [MsgAccountSRP6Ex](msgaccountsrp6ex.md) | Requests SRP6 password exchange |
| 2030 | [MsgNpcInfo](msgnpcinfo.md) | NPC spawn information |
| 2031 | [MsgNpc](msgnpc.md) |  |
| 2032 | [MsgTaskDialog](msgtaskdialog.md) |  |
| 2033 | [MsgFriendInfo](msgfriendinfo.md) |  |
| 2035 | [MsgPetInfo](msgpetinfo.md) |  |
| 2036 | [MsgDataArray](msgdataarray.md) |  |
| 2041 | [MsgAnnounceList](msgannouncelist.md) |  |
| 2042 | [MsgAnnounceInfo](msgannounceinfo.md) |  |
| 2043 | [MsgTrainingInfo](msgtraininginfo.md) |  |
| 2044 | [MsgTraining](msgtraining.md) |  |
| 2045 | [MsgAuraGroup](msgauragroup.md) |  |
| 2046 | [MsgTradeBuddy](msgtradebuddy.md) |  |
| 2047 | [MsgTradeBuddyInfo](msgtradebuddyinfo.md) |  |
| 2048 | [MsgEquipLock](msgequiplock.md) |  |
| 2050 | [MsgPigeon](msgpigeon.md) |  |
| 2051 | [MsgPigeonQuery](msgpigeonquery.md) |  |
| 2064 | [MsgPeerage](msgpeerage.md) |  |
| 2065 | [MsgGuide](msgguide.md) |  |
| 2066 | [MsgGuideInfo](msgguideinfo.md) |  |
| 2067 | [MsgContribute](msgcontribute.md) |  |
| 2068 | [MsgQuiz](msgquiz.md) |  |
| 2069 | [MsgQuizSponsor](msgquizsponsor.md) |  |
| 2070 | [MsgSuitStatus](msgsuitstatus.md) |  |
| 2071 | [MsgRelation](msgrelation.md) |  |
| 2072 | [MsgRaceTrackProp](msgracetrackprop.md) |  |
| 2073 | [MsgRaceTrackPropEffect](msgracetrackpropeffect.md) |  |
| 2075 | [MsgRaceTrackStatus](msgracetrackstatus.md) |  |
| 2076 | [MsgQuench](msgquench.md) |  |
| 2077 | [MsgItemStatus](msgitemstatus.md) |  |
| 2078 | [MsgUserIPInfo](msguseripinfo.md) |  |
| 2079 | [MsgServerInfo](msgserverinfo.md) |  |
| 2080 | [MsgChangeName](msgchangename.md) |  |
| 2081 | [MsgDeadMark](msgdeadmark.md) |  |
| 2082 | [MsgUserCityInfo](msgusercityinfo.md) |  |
| 2090 | [MsgShowHandEnter](msgshowhandenter.md) |  |
| 2091 | [MsgShowHandDealtCard](msgshowhanddealtcard.md) |  |
| 2092 | [MsgShowHandActivePlayer](msgshowhandactiveplayer.md) |  |
| 2093 | [MsgShowHandCallAction](msgshowhandcallaction.md) |  |
| 2094 | [MsgShowHandLayCard](msgshowhandlaycard.md) |  |
| 2095 | [MsgShowHandGameResult](msgshowhandgameresult.md) |  |
| 2096 | [MsgShowHandExit](msgshowhandexit.md) |  |
| 2097 | [MsgShowHandOnlineStatus](msgshowhandonlinestatus.md) |  |
| 2098 | [MsgShowHandLostInfo](msgshowhandlostinfo.md) |  |
| 2099 | [MsgShowHandTrusteeship](msgshowhandtrusteeship.md) |  |
| 2101 | [MsgFactionRankInfo](msgfactionrankinfo.md) |  |
| 2102 | [MsgSynMemberList](msgsynmemberlist.md) |  |
| 2103 | [MsgSynChgDomName](msgsynchgdomname.md) |  |
| 2110 | [MsgSuperFlag](msgsuperflag.md) |  |
| 2170 | [MsgLeaveWord](msgleaveword.md) |  |
| 2171 | [MsgTexasInteractive](msgtexasinteractive.md) |  |
| 2172 | [MsgTexasNpcInfo](msgtexasnpcinfo.md) |  |
| 2201 | [MsgTotemPoleInfo](msgtotempoleinfo.md) |  |
| 2202 | [MsgWeaponsInfo](msgweaponsinfo.md) |  |
| 2203 | [MsgTotemPole](msgtotempole.md) |  |
| 2205 | [MsgQualifyingInteractive](msgqualifyinginteractive.md) |  |
| 2206 | [MsgQualifyingFightersList](msgqualifyingfighterslist.md) |  |
| 2207 | [MsgQualifyingRank](msgqualifyingrank.md) |  |
| 2208 | [MsgQualifyingSeasonRankList](msgqualifyingseasonranklist.md) |  |
| 2209 | [MsgQualifyingDetailInfo](msgqualifyingdetailinfo.md) |  |
| 2210 | [MsgArenicScore](msgarenicscore.md) |  |
| 2211 | [MsgArenicWitness](msgarenicwitness.md) |  |
| 2218 | [MsgElitePKArenic](msgelitepkarenic.md) |  |
| 2219 | [MsgPKEliteMatchInfo](msgpkelitematchinfo.md) |  |
| 2220 | [MsgPKStatistic](msgpkstatistic.md) |  |
| 2221 | [MsgPKEnable](msgpkenable.md) |  |
| 2222 | [MsgElitePKScore](msgelitepkscore.md) |  |
| 2223 | [MsgElitePKGameRankInfo](msgelitepkgamerankinfo.md) |  |
| 2224 | [MsgWarFlag](msgwarflag.md) |  |
| 2225 | [MsgSynRecruitAdvertising](msgsynrecruitadvertising.md) |  |
| 2226 | [MsgSynRecruitAdvertisingList](msgsynrecruitadvertisinglist.md) |  |
| 2227 | [MsgSynRecruitAdvertisingOpt](msgsynrecruitadvertisingopt.md) |  |
| 2230 | [MsgTeamPKArenic](msgteampkarenic.md) |  |
| 2231 | [MsgTeamPKArenicScore](msgteampkarenicscore.md) |  |
| 2232 | [MsgTeamPKMatchInfo](msgteampkmatchinfo.md) |  |
| 2233 | [MsgTeamPKRankInfo](msgteampkrankinfo.md) |  |
| 2240 | [MsgDominateTeamName](msgdominateteamname.md) |  |
| 2241 | [MsgTeamArenaInteractive](msgteamarenainteractive.md) |  |
| 2242 | [MsgTeamArenaFightingTeamList](msgteamarenafightingteamlist.md) |  |
| 2243 | [MsgTeamArenaRank](msgteamarenarank.md) |  |
| 2244 | [MsgTeamArenaYTop10List](msgteamarenaytop10list.md) |  |
| 2245 | [MsgTeamArenaHeroData](msgteamarenaherodata.md) |  |
| 2246 | [MsgTeamArenaScore](msgteamarenascore.md) |  |
| 2247 | [MsgTeamArenaFightingMemberInfo](msgteamarenafightingmemberinfo.md) |  |
| 2250 | [MsgTeamPopPKArenic](msgteampoppkarenic.md) |  |
| 2251 | [MsgTeamPopPKArenicScore](msgteampoppkarenicscore.md) |  |
| 2252 | [MsgTeamPopPKMatchInfo](msgteampoppkmatchinfo.md) |  |
| 2253 | [MsgTeamPopPKRankInfo](msgteampoppkrankinfo.md) |  |
| 2260 | [MsgDominateTeamPopPkName](msgdominateteampoppkname.md) |  |
| 2261 | [Msg2ndPsw](msg2ndpsw.md) |  |
| 2262 | [MsgPaint](msgpaint.md) |  |
| 2286 | [MsgMapItem](msgmapitem.md) |  |
| 2320 | [MsgSubPro](msgsubpro.md) |  |
| 2330 | [MsgFactionMatch](msgfactionmatch.md) |  |
| 2331 | [MsgFMRoundRobin](msgfmroundrobin.md) |  |
| 2332 | [MsgFMMatch](msgfmmatch.md) |  |
| 2333 | [MsgFactionMatchWitness](msgfactionmatchwitness.md) |  |
| 2400 | [MsgTransportor](msgtransportor.md) |  |
| 2401 | [MsgInstance](msginstance.md) |  |
| 2410 | [MsgAura](msgaura.md) |  |
| 2420 | [MsgVerifyCheck](msgverifycheck.md) |  |
| 2430 | [MsgNationality](msgnationality.md) |  |
| 2501 | [MsgCrossSwitch](msgcrossswitch.md) |  |
| 2502 | [MsgCrossFlagWar](msgcrossflagwar.md) |  |
| 2504 | [MsgCrossFlagWarMerit](msgcrossflagwarmerit.md) |  |
| 2505 | [MsgCrossFlagWarAltar](msgcrossflagwaraltar.md) |  |
| 2506 | [MsgCrossFlagWarFlag](msgcrossflagwarflag.md) |  |
| 2507 | [MsgCrossFlagWarRank](msgcrossflagwarrank.md) |  |
| 2510 | [MsgFactionChiefBase](msgfactionchiefbase.md) |  |
| 2521 | [MsgKickOut](msgkickout.md) |  |
| 2533 | [MsgTrainingVitality](msgtrainingvitality.md) |  |
| 2534 | [MsgTrainingVitalityInfo](msgtrainingvitalityinfo.md) |  |
| 2535 | [MsgTrainingVitalityScore](msgtrainingvitalityscore.md) |  |
| 2600 | [MsgGLRankingList](msgglrankinglist.md) |  |
| 2601 | [MsgGLHeroDetail](msgglherodetail.md) |  |
| 2602 | [MsgGLLastSeasonTopScore](msggllastseasontopscore.md) |  |
| 2603 | [MsgGLChampionList](msgglchampionlist.md) |  |
| 2604 | [MsgGLInteractive](msgglinteractive.md) |  |
| 2700 | [MsgOwnKongfuBase](msgownkongfubase.md) |  |
| 2701 | [MsgOwnKongfuImproveSummaryInfo](msgownkongfuimprovesummaryinfo.md) |  |
| 2702 | [MsgOwnKongfuImproveFeedback](msgownkongfuimprovefeedback.md) |  |
| 2703 | [MsgOwnKongRank](msgownkongrank.md) |  |
| 2704 | [MsgOwnKongfuPKSetting](msgownkongfupksetting.md) |  |
| 2710 | [MsgMagicCoat](msgmagiccoat.md) |  |
