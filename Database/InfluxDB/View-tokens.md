### 查看Token

命令行界面-查看Token
```text
influx auth find
```

例：
```text
[root@bogon bin]# influx auth find
ID			Token												Status	User UserID			Permissions
04c41ebc21eae000	RZYV7Et3jcyuOfNvHYsxZS9HfdBhJ2rcvvFP3Vg7xmclDpSFnbcTz-WizgIkrBRPTNxEEtzhXen0Qw2L12ZmOw==	active	<nil>04c41ebc0ceae000	[read:authorizations write:authorizations read:buckets write:buckets read:dashboards write:dashboards read:orgs write:orgs read:sources write:sources read:tasks write:tasks read:telegrafs write:telegrafs read:users write:users read:variables write:variables read:scrapers write:scrapers read:secrets write:secrets read:labels write:labels read:views write:views read:documents write:documents read:notificationRules write:notificationRules read:notificationEndpoints write:notificationEndpoints read:checks write:checks]
```