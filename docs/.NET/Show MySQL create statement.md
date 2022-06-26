## RepoDB

```fsharp
#r "nuget: RepoDb.MySQL"
#r "nuget: wk.DynamicTables"
#load "ConnectionString.fsx"

open MySql.Data.MySqlClient
open RepoDb
open RepoDb.Attributes
open System.Linq

type Create = {
    Table: string
    [<Map("Create Table")>]
    CreateTable: string
}

RepoDb.MySqlBootstrap.Initialize()

let showCreate(db: string, table: string) =
    let connection = new MySqlConnection(ConnectionString.MyConnection)
    let output =
        let cmd = $"show create table {db}.{table}"
        connection.ExecuteQuery<Create>(cmd).First()
    printfn "%s" output.CreateTable

showCreate("alfresco", "alf_child_assoc")
```

Output

```sql
CREATE TABLE `alf_child_assoc` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `version` bigint(20) NOT NULL,
  `parent_node_id` bigint(20) NOT NULL,
  `type_qname_id` bigint(20) NOT NULL,
  `child_node_name_crc` bigint(20) NOT NULL,
  `child_node_name` varchar(50) NOT NULL,
  `child_node_id` bigint(20) NOT NULL,
  `qname_ns_id` bigint(20) NOT NULL,
  `qname_localname` varchar(255) NOT NULL,
  `qname_crc` bigint(20) NOT NULL,
  `is_primary` bit(1) DEFAULT NULL,
  `assoc_index` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `parent_node_id` (`parent_node_id`,`type_qname_id`,`child_node_name_crc`,`child_node_name`),
  KEY `idx_alf_cass_pnode` (`parent_node_id`,`assoc_index`,`id`),
  KEY `fk_alf_cass_cnode` (`child_node_id`),
  KEY `fk_alf_cass_tqn` (`type_qname_id`),
  KEY `fk_alf_cass_qnns` (`qname_ns_id`),
  KEY `idx_alf_cass_qncrc` (`qname_crc`,`type_qname_id`,`parent_node_id`),
  KEY `idx_alf_cass_pri` (`parent_node_id`,`is_primary`,`child_node_id`),
  CONSTRAINT `fk_alf_cass_cnode` FOREIGN KEY (`child_node_id`) REFERENCES `alf_node` (`id`),
  CONSTRAINT `fk_alf_cass_pnode` FOREIGN KEY (`parent_node_id`) REFERENCES `alf_node` (`id`),
  CONSTRAINT `fk_alf_cass_qnns` FOREIGN KEY (`qname_ns_id`) REFERENCES `alf_namespace` (`id`),
  CONSTRAINT `fk_alf_cass_tqn` FOREIGN KEY (`type_qname_id`) REFERENCES `alf_qname` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=70955 DEFAULT CHARSET=utf8
```