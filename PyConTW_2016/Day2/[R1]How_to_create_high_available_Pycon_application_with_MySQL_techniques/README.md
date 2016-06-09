## Talk: How to create high available Pycon application with MySQL techniques
- Info: https://tw.pycon.org/2016/events/talk/39346130420498441/
- Speaker: 杜修文
- MySQL 高可用階層（可用性由上往下遞增）
	- Replication
	- Shared Disk / Virtualization Options
	- Group Replication
	- Cluster

- MySQL Fabric
	- 做data shared
	- Fabric aware connection（支援java，php，python） 或是使用 MySQL Route

- MySQL 5.7可做多源複製：
	- 使用場景，當有很多分公司或是搜集資料的master db，可以把資料都回傳給主公司的slave

- Group Replication
	- 只支援InnoDB
	- 每個表都要有pk
	- 需要開啟GTID
	- 不能線上同時多地DDL
	- 交易會因為跟其他台衝突而中止

- Cluster（架構由上而下）
	- client（PHP,python）
	- Application （MySQL, apache, java, nodes）
	- Data node