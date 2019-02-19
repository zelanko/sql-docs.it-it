---
title: Sys. database_firewall_rules (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c044294b7bb9beb8de502b3a1148c55dd026ab02
ms.sourcegitcommit: ca9b5cb6bccfdba4cdbe1697adf5c673b4713d6c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/18/2019
ms.locfileid: "56407601"
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sulle impostazioni del firewall a livello di database associati con il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Le impostazioni del firewall a livello di database sono particolarmente utili quando si usano utenti del database indipendente. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 La vista `sys.database_firewall_rules` contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|Identificatore dell'impostazione del firewall a livello di database.|  
|NAME|**NVARCHAR(128)**|Il nome scelto per descrivere e distinguere l'impostazione del firewall a livello di database.|  
|start_ip_address|**VARCHAR(50)**|L'indirizzo IP più basso nell'intervallo dell'impostazione del firewall a livello di database. Gli indirizzi IP uguali o maggiori di questo possono tentare la connessione all'istanza del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più basso possibile è `0.0.0.0`.|  
|end_ip_address|**VARCHAR(50)**|L'indirizzo IP più alto nell'intervallo dell'impostazione del firewall. Gli indirizzi IP uguali o minori di questo possono tentare la connessione all'istanza del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più alto possibile è `255.255.255.255`.<br /><br /> Nota: Tentativi di connessione Windows Azure sono consentiti quando sia questo campo e il **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**DATETIME**|Data e ora UTC in cui è stata creata l'impostazione del firewall a livello di database.|  
|modify_date|**DATETIME**|Data e ora UTC in cui è stata modificata per l'ultima volta l'impostazione del firewall a livello di database.|  
  
## <a name="remarks"></a>Note  
 Per rimuovere una regola del firewall del database, usare [sp_delete_database_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md). Per impostare una regola del firewall per tutti [!INCLUDE[ssSDS](../../includes/sssds-md.md)], vedere [sp_set_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md). Per restituire informazioni sui database esistente di regole del firewall, eseguire una query [Sys. database_firewall_rules (Database SQL di Azure)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissions  
 Questa vista è disponibile nel **master** database e in ogni database utente. L'accesso di sola lettura a questa vista è disponibile per tutti gli utenti che dispongono dell'autorizzazione per connettersi al database.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_set_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys. database_firewall_rules (Database SQL di Azure)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Configurare un Firewall di Windows per l'accesso al motore di Database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurare un Firewall per l'accesso FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
