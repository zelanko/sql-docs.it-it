---
title: sp_delete_firewall_rule (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 406f94ab0ab2d0ebaddf9635448e364bf90ceb8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032787"
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Rimuove le impostazioni del firewall a livello di server dal server del [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Questa stored procedure è disponibile solo nel database master all'account di accesso principale di livello server.  

  
## <a name="syntax"></a>Sintassi  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>Argomenti  
 L'argomento della stored procedure è:  
  
 [@name =] '*nome*'  
 Nome dell'impostazione del firewall a livello di server che verrà rimossa. *nome* viene **nvarchar (128)** non prevede alcun valore predefinito.  
  
## <a name="remarks"></a>Note  
 Nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)] i dati dell'account di accesso necessari per autenticare una connessione e le regole del firewall a livello di server vengono memorizzati temporaneamente nella cache in ogni database. Questa cache viene aggiornata periodicamente. Per forzare un aggiornamento della cache di autenticazione e assicurarsi che un database abbia la versione più recente della tabella di account di accesso, eseguire [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Solo l'account di accesso dell'entità di livello server creato dal processo di provisioning può eliminare le regole firewall a livello di server. L'utente deve essere connesso al database master per l'esecuzione sp_delete_firewall_rule.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene rimossa l'impostazione del firewall a livello di server denominata 'Impostazione di esempio 1'. Eseguire l'istruzione nel database master virtuale.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Firewall del Database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Procedura: Configurare le impostazioni del Firewall (Database SQL di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys. firewall_rules &#40;Database SQL di Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


