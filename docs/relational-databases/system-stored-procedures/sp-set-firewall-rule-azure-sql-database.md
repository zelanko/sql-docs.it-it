---
title: sp_set_firewall_rule (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: a096814c7d037fe517614e2701d5a821edcaa053
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024692"
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Crea o aggiorna le impostazioni del firewall a livello di server per il server del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Questa stored procedure è disponibile solo nel database master all'account di accesso entità a livello di server o all'entità di Azure Active Directory assegnato.  
  
  
## <a name="syntax"></a>Sintassi  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 Nella tabella seguente vengono illustrati gli argomenti supportati e le opzioni presenti nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|nome|Datatype|Descrizione|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR(128)**|Nome utilizzato per descrivere e distinguere l'impostazione del firewall a livello di server.|  
|[@start_ip_address =] 'start_ip_address'|**VARCHAR(50)**|L'indirizzo IP più basso nell'intervallo dell'impostazione del firewall a livello di server. Gli indirizzi IP uguali o maggiori di questo possono tentare la connessione al server del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più basso possibile è `0.0.0.0`.|  
|[@end_ip_address =] 'end_ip_address'|**VARCHAR(50)**|L'indirizzo IP più alto nell'intervallo dell'impostazione del firewall a livello di server. Gli indirizzi IP uguali o minori di questo possono tentare la connessione al server del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più alto possibile è `255.255.255.255`.<br /><br /> Nota: Tentativi di connessione di Azure sono consentiti quando sia questo campo e il *start_ip_address* campo equals `0.0.0.0`.|  
  
## <a name="remarks"></a>Note  
 I nomi delle impostazioni del firewall a livello di server devono essere univoci. Se il nome dell'impostazione fornito per la stored procedure esiste già nella tabella delle impostazioni del firewall, gli indirizzi IP iniziale e finale verranno aggiornati. In caso contrario, verrà creata una nuova impostazione del firewall a livello di server.  
  
 Quando si aggiunge un'impostazione del firewall a livello di server in cui sono uguali a iniziale e finale degli indirizzi IP `0.0.0.0`, è possibile accedere al [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server da Azure. Specificare un valore per il *nome* parametro che consenta di ricordare che cos'è l'impostazione del firewall a livello di server per.  
  
 Nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)] i dati dell'account di accesso necessari per autenticare una connessione e le regole del firewall a livello di server vengono memorizzati temporaneamente nella cache in ogni database. Questa cache viene aggiornata periodicamente. Per forzare un aggiornamento della cache di autenticazione e assicurarsi che un database abbia la versione più recente della tabella di account di accesso, eseguire [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Solo l'accesso. dell'entità a livello di server creati dal processo di provisioning o un'entità di Azure Active Directory assegnato come amministratore è possibile creare o modificare le regole firewall a livello di server. L'utente deve essere connesso al database master per eseguire sp_set_firewall_rule.  
  
## <a name="examples"></a>Esempi  
 Il codice seguente crea un firewall di livello server denominata `Allow Azure` che abilita l'accesso da Azure. Eseguire il codice seguente nel database master virtuale.  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 Il codice seguente consente di creare un'impostazione del firewall a livello di server denominata `Example setting 1` solo per l'indirizzo IP `0.0.0.2`. Successivamente, il `sp_set_firewall_rule` stored procedure viene chiamata nuovamente per aggiornare l'indirizzo IP finale per `0.0.0.4`, in quanto impostazione del firewall. Ciò consente di creare un intervallo che consente gli indirizzi IP `0.0.0.2`, `0.0.0.3`, e `0.0.0.4` per accedere al server.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Firewall del Database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Procedura: Configurare le impostazioni del Firewall (Database SQL di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [Sys. firewall_rules &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
