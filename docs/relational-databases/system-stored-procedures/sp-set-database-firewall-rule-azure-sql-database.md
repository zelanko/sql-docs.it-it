---
title: sp_set_database_firewall_rule (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: e5363e741c827a0fb16528a8b617e26a5b95f8a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025696"
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Crea o aggiorna le regole del firewall a livello di database per il [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Regole firewall del database possono essere configurate per il **master** database e per i database utente sul [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Regole firewall del database sono particolarmente utili quando usando utenti del database indipendente. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 **[@name**  =] [N]'*nome*'  
 Il nome utilizzato per descrivere e distinguere l'impostazione del firewall a livello di database. *nome* viene **nvarchar (128)** non prevede alcun valore predefinito. L'identificatore di Unicode `N` è facoltativo per [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. 
  
 **[@start_ip_address** =] '*start_ip_address*'  
 L'indirizzo IP più basso nell'intervallo dell'impostazione del firewall a livello di database. Gli indirizzi IP uguali o maggiori di questo possono tentare la connessione all'istanza del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più basso possibile è `0.0.0.0`. *start_ip_address* viene **varchar (50)** non prevede alcun valore predefinito.  
  
 [ **@end_ip_address** =] '*end_ip_address*'  
 L'indirizzo IP più alto nell'intervallo dell'impostazione del firewall a livello di database. Gli indirizzi IP uguali o minori di questo possono tentare la connessione all'istanza del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. L'indirizzo IP più alto possibile è `255.255.255.255`. *end_ip_address* viene **varchar (50)** non prevede alcun valore predefinito.  
  
 Nella tabella seguente vengono illustrati gli argomenti supportati e le opzioni presenti nella [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
> [!NOTE]  
>  Tentativi di connessione di Azure sono consentiti quando sia questo campo e il *start_ip_address* campo equals `0.0.0.0`.  
  
## <a name="remarks"></a>Note  
 I nomi delle impostazioni del firewall a livello di database per un database devono essere univoci. Se il nome dell'impostazione del firewall a livello di database fornito per la stored procedure esiste già nella tabella delle impostazioni del firewall a livello di database, gli indirizzi IP iniziale e finale verranno aggiornati. In caso contrario, verrà creata un'impostazione del firewall a livello di database.  
  
 Quando si aggiunge un'impostazione del firewall a livello di database in cui sono uguali a iniziale e finale degli indirizzi IP `0.0.0.0`, si abilita l'accesso al database nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server da qualsiasi risorsa di Azure. Specificare un valore per il *nome* parametro che consenta di ricordare che cos'è l'impostazione del firewall per.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione **CONTROL** per il database.  
  
## <a name="examples"></a>Esempi  
 Il codice seguente crea un firewall di livello database denominata `Allow Azure` che abilita l'accesso al database di Azure.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 Il codice seguente consente di creare un'impostazione del firewall a livello di database denominata `Example DB Setting 1` solo per l'indirizzo IP `0.0.0.4`. Successivamente, il `sp_set_database firewall_rule` stored procedure viene chiamata nuovamente per aggiornare l'indirizzo IP finale per `0.0.0.6`, in quanto impostazione del firewall. Ciò consente di creare un intervallo che consente gli indirizzi IP `0.0.0.4`, `0.0.0.5`, e `0.0.0.6` per accedere al database.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Firewall del Database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Procedura: Configurare le impostazioni del Firewall (Database SQL di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Sys. database_firewall_rules &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
