---
title: Sys. firewall_rules (Database SQL di Azure) | Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5127dacf628231199c5ce5ac49fdb2377c82f270
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631621"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sulle impostazioni del firewall a livello di server associato con il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 La vista `sys.firewall_rules` contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|id|**INT**|Identificatore dell'impostazione del firewall a livello di server.|  
|NAME|**NVARCHAR(128)**|Nome scelto per descrivere e distinguere l'impostazione del firewall a livello di server.|  
|start_ip_address|**VARCHAR(45)**|L'indirizzo IP più basso nell'intervallo dell'impostazione del firewall a livello di server. Gli indirizzi IP uguali o maggiori di questo possono tentare la connessione al server del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più basso possibile è `0.0.0.0`.|  
|end_ip_address|**VARCHAR(45)**|L'indirizzo IP più alto nell'intervallo dell'impostazione del firewall a livello di server. Gli indirizzi IP uguali o minori di questo possono tentare la connessione al server del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più alto possibile è `255.255.255.255`.<br /><br /> Nota: Tentativi di connessione Windows Azure sono consentiti quando sia questo campo e il **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**DATETIME**|Data e ora UTC in cui è stata creata l'impostazione del firewall a livello di server.<br /><br /> Nota: UTC è l'acronimo di Coordinated Universal Time.|  
|modify_date|**DATETIME**|Data e ora UTC in cui è stata modificata per l'ultima volta l'impostazione del firewall a livello di server.|  
  
## <a name="remarks"></a>Note

 Restituire informazioni sulle impostazioni del firewall a livello di database associati al Database SQL di Microsoft Azure, usare [Sys. database_firewall_rules &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissions

 Accesso in lettura a questa vista è disponibile per tutti gli utenti con autorizzazione per connettersi al **master** database.  
  
## <a name="see-also"></a>Vedere anche

[sp_set_firewall_rule &#40;Database di SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Database di SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[Sys. database_firewall_rules &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[Configurare un Firewall di Windows per l'accesso al motore di Database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurare un firewall per l'accesso FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
