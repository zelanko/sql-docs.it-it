---
title: sp_set_database_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 08/04/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: dfe41ee68412414df24bc7f0bd583bbb0109b3db
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055086"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Crea o aggiorna le regole del firewall a livello di database per la [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Le regole del firewall del database possono essere configurate per il database **Master** e per i database utente in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Le regole del firewall del database sono particolarmente utili quando si usano gli utenti del database indipendente. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] [N]'name'` il nome utilizzato per descrivere e distinguere l'impostazione del firewall a livello di database. *Name* è di **tipo nvarchar (128)** e non prevede alcun valore predefinito. L'identificatore Unicode `N` è facoltativo per [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. 
  
`[ @start_ip_address = ] 'start_ip_address'` l'indirizzo IP più basso nell'intervallo dell'impostazione del firewall a livello di database. Gli indirizzi IP uguali o maggiori di questo possono tentare la connessione all'istanza del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più basso possibile è `0.0.0.0`. *start_ip_address* è di tipo **varchar (50)** e non prevede alcun valore predefinito.  
  
`[ @end_ip_address = ] 'end_ip_address'` l'indirizzo IP più alto nell'intervallo dell'impostazione del firewall a livello di database. Gli indirizzi IP uguali o minori di questo possono tentare la connessione all'istanza del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più alto possibile è `255.255.255.255`. *end_ip_address* è di tipo **varchar (50)** e non prevede alcun valore predefinito.  
  
 Nella tabella seguente vengono illustrati gli argomenti e le opzioni supportati in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
> [!NOTE]  
>  I tentativi di connessione di Azure sono consentiti quando sia questo campo che il campo *start_ip_address* sono uguali `0.0.0.0`.  
  
## <a name="remarks"></a>Osservazioni  
 I nomi delle impostazioni del firewall a livello di database per un database devono essere univoci. Se il nome dell'impostazione del firewall a livello di database fornito per la stored procedure esiste già nella tabella delle impostazioni del firewall a livello di database, gli indirizzi IP iniziale e finale verranno aggiornati. In caso contrario, verrà creata un'impostazione del firewall a livello di database.  
  
 Quando si aggiunge un'impostazione del firewall a livello di database in cui gli indirizzi IP iniziale e finale sono uguali a `0.0.0.0`, si Abilita l'accesso al database nel server [!INCLUDE[ssSDS](../../includes/sssds-md.md)] da qualsiasi risorsa di Azure. Fornire un valore al parametro *Name* che consenta di ricordare l'impostazione del firewall per.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione **CONTROL** per il database.  
  
## <a name="examples"></a>Esempi  
 Il codice seguente crea un'impostazione del firewall a livello di database denominata `Allow Azure` che consente l'accesso al database da Azure.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 Il codice seguente consente di creare un'impostazione del firewall a livello di database denominata `Example DB Setting 1` solo per l'indirizzo IP `0.0.0.4`. Quindi, il `sp_set_database firewall_rule` stored procedure viene richiamato per aggiornare l'indirizzo IP finale a `0.0.0.6`, in tale impostazione del firewall. Viene creato un intervallo che consente agli indirizzi IP `0.0.0.4`, `0.0.0.5`e `0.0.0.6` di accedere al database.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>Vedere anche  
   del [firewall del database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)  
 [Procedura: configurare le impostazioni del firewall (database SQL di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40; &#41; database SQL di Azure](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
 [sp_delete_database_firewall_rule &#40; &#41; database SQL di Azure](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
 [sys. database_firewall_rules &#40;database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
