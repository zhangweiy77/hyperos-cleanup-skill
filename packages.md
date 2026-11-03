# 包名单（实测账本）

说明：包名是给 AI 和电脑命令用的；「人话」是给人看的。状态是我们在一台 Redmi Note 15 Pro+（澎湃 OS 3）上的实测结果。你的手机上名单会有出入——永远以你自己手机的盘点为准。

## 一、红线 · 别碰（卸了会出大事）

| 包名 | 人话 | 为什么别碰 |
|---|---|---|
| `com.miui.packageinstaller` | 装应用的核心组件 | 卸了装不了应用，天大的事 |
| `com.miui.securitycore` | 安全核心 | 管着应用双开、应用锁的后台，管家都卸了它都得留 |
| `com.lbe.security.miui` | 权限管理引擎 | 系统权限页面的发动机 |
| `com.miui.powerkeeper` | 电量与性能 | 省电主干，卸了续航会出问题 |
| `com.xiaomi.xmsf` | 小米推送框架 | 微信等应用的消息推送靠它，卸了消息会迟到甚至收不到 |
| `com.miui.tsmclient` | 小米智能卡 | 手机里的公交卡、门卡靠它刷 |
| `org.codeaurora.ims` | 真正的通话核心 | VoLTE 高清通话本体，卸了打不了电话 |
| `com.xiaomi.misettings` | 小米设置组件 | 设置里很多页面靠它 |
| `com.android.phone` / `com.android.systemui` 等 | 系统框架件 | 名字带 android 的基础件，一律不碰 |

## 二、留壳特例（不能整卸，要特殊处理）

| 包名 | 人话 | 处理法 |
|---|---|---|
| `com.miui.securitycenter` | 手机管家（安全中心） | **整卸会导致系统选照片功能崩溃**（见 SKILL.md 的 R4）。正确做法：包留着，用 `cmd jobscheduler cancel com.miui.securitycenter 20001` 取消它的 FBO 数据收集任务（任务号以你手机上 `dumpsys jobscheduler` 查到的为准）；用户再在应用里撤回隐私同意。它的权限是系统焊死的，收不回来（R5），认了。 |

## 三、已清 · 主空间（47 件，全部实测可卸、功能无损）

### 数据收集与上报（核心目标）
| 包名 | 人话 |
|---|---|
| `com.miui.analytics` | 小米的数据统计（激活和使用情况上报） |
| `com.miui.misightservice` | 系统故障与使用数据采集 |
| `com.xiaomi.security.onetrack` | OneTrack 数据上报通道 |
| `com.miui.uireporter` | UI 使用信息上报工具 |
| `com.miui.bugreport` | 问题反馈上报 |
| `com.miui.bsp.catchlog` | 系统日志抓取 |
| `com.miui.daemon` | 小米后台守护（含统计与云控通道） |
| `com.xiaomi.registration` | 设备注册上报 |
| `com.xiaomi.ab` | AB 实验分流（给你分组做实验的） |
| `com.miui.hybrid` | 快应用/混合服务框架（带数据服务） |
| `com.miui.systemAdSolution` | 系统广告方案组件 |
| `com.android.adservices.api` | 广告服务接口（个性化广告那套） |
| `com.android.ondevicepersonalization.services` | 设备端个性化服务（广告画像） |
| `com.android.federatedcompute.services` | 联合计算服务（广告画像训练） |

### 运营商与网络相关
| 包名 | 人话 |
|---|---|
| 运营商探针件（实测机上名为 `mobiletools.systemhelper`，完整包名以你自己手机的盘点为准） | 运营商定制探针，收集使用信息——和正规运营商服务不是一回事，先查实身份再卸（R13） |
| `com.xiaomi.dmregservice` | 设备管理注册服务（卸后必须验活：双卡在网、能打电话、能收验证码） |
| `com.xiaomi.metoknlp` | 运营商网络定位辅助（卸后定位变化见 R10） |
| `com.qti.qms.service.connectionsecurity` | 高通连接安全服务（附加件） |
| `com.qti.qms.service.trustzoneaccess` | 高通信任区访问服务（附加件） |
| `com.qti.server.qtiwifi` | 高通 Wi-Fi 附加服务 |
| `com.xiaomi.simactivate.service` | 小米 SIM 卡激活服务 |

### 小米账号与云（要按顺序：先让用户退出登录，再卸这一串，见 R3）
| 包名 | 人话 |
|---|---|
| `com.xiaomi.account` | 小米账号本体 |
| `com.miui.cloudservice` | 小米云服务 |
| `com.miui.micloudsync` | 小米云同步 |
| `com.miui.cloudbackup` | 小米云备份 |
| `com.xiaomi.finddevice` | 查找设备（注意它和账号页的连带关系，R3） |

### 语音与 AI 附加件
| 包名 | 人话 |
|---|---|
| `com.miui.voiceassist` | 超级小爱（语音助手本体）。注意别和它的外壳组件 `voiceassistProxy` 搞混，查询要精确匹配（R2） |
| `com.miui.voicetrigger` | 语音唤醒 |
| `com.xiaomi.aicr` | AI 识别服务 |
| `com.xiaomi.aireco` | AI 推荐服务 |
| `com.xiaomi.aiasst.service` | AI 助理服务 |
| `com.xiaomi.aiasst.vision` | AI 视觉服务 |
| `com.xiaomi.aon` | 常开感知（Always-on）服务 |

### 推荐、广告与内容位
| 包名 | 人话 |
|---|---|
| `com.miui.personalassistant` | 智能助理（负一屏推荐） |
| `com.miui.yellowpage` | 生活黄页（来电识别那摊，官方都写了可禁用） |
| `com.miui.contentextension` | 内容扩展（传送门相关） |
| `com.miui.wmsvc` | 壁纸/内容服务组件 |
| `com.xiaomi.gamecenter.sdk.service` | 游戏服务 SDK（游戏中心本体早就不在了，剩个壳子在跑） |
| `com.miui.nextpay` | 小米支付（NFC 刷卡是智能卡管的，和它无关） |
| `com.xiaomi.barrage` | 弹幕通知（把通知内容做成弹幕飘过去的花活） |
| `com.android.browser` | 小米浏览器（卸前先确认默认浏览器已是 Chrome 等其他浏览器） |

### 其他
| 包名 | 人话 |
|---|---|
| `com.miui.greenguard` | 家人守护（远程守护家里老人小孩的，和儿童空间不是一回事） |
| `com.miui.guardprovider` | 安全服务（安装流程相关，卸后注意 R15 的观察项：装应用若异常先把它装回来） |
| `com.xiaomi.joyose` | 游戏加速的云控组件 |
| `com.xiaomi.touchservice` | 触控采样服务 |
| `com.xiaomi.location.fused` | 小米融合定位（卸后定位变化见 R10） |
| `com.xiaomi.xmsfkeeper` | 推送框架的日志员（卸后进程可能赖着不走，R9，重启即消） |

## 四、已清 · 分身空间（1 件）

| 命令 | 人话 |
|---|---|
| `pm uninstall --user 999 com.miui.analytics` | 分身空间里那份数据统计。双开空间有独立名单，主空间清完别忘了它（R12） |

## 五、禁用中和（硬卸被系统拒绝，先冻住，待重启后重试硬卸，见 R8）

| 包名 | 人话 |
|---|---|
| `com.mfashiongallery.emag` | 小米画报（锁屏轮播广告杂志） |
| `com.miui.cleanmaster` | 垃圾清理（手机管家的清理子应用） |

处理命令：`pm disable-user --user 0 <包名>`。禁用后进程停止、不再运行，效果等同卸载，只是包体还躺在系统里。

## 六、看情况 · 我们没动的

| 包名 | 人话 | 为什么没动 |
|---|---|---|
| `com.miui.passwords` | 小米密码（密码保管箱） | 万一用户在里面存过密码，卸了就找不回来。必须先问清用户存没存过 |
| `com.xiaomi.market` | 应用商店 | 小米系应用的更新通道（R14），留不留让用户选 |
| `com.qualcomm.qti.devicestatisticsservice` | 高通设备统计 | 确实会发统计，但量小、各方实测共识是保留，收益不抵风险 |
| `com.xiaomi.micloud.sdk` | 小米云的共享库 | 云服务都清完之后它就是个没人调用的死库；名单评级是「别碰」，不值得冒险 |
| `com.miui.backup` | 本地备份 | 正经的保险功能，不往外发 |
| `com.xiaomi.hypercomm` / `com.miui.carlink` / `com.milink.service` | 互联互通那一套 | 车机互联、跨屏协同的功能件，用不用看用户 |
| `com.miui.aod` | 息屏显示 | 功能件，不是收集件 |

---

最后一句大白话：这份名单的价值不在「全」，在于每一条后面都写了**为什么**和**出事了怎么办**。你的手机和我们的不完全一样，多出来的、没见过的，先查清再决定——查不清的，就先留着。干净是慢慢来的，手机是天天用的。
