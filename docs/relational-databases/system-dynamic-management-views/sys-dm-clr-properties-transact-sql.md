---
title: sys.dm_clr_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 331969c2baa8ec67e0cd7c0ebf8cdd894878f397
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266058"
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Restituisce una riga per ogni proprietà associata all'integrazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Common Language Runtime (CLR), inclusi la versione e lo stato del CLR hosted. Il CLR hosted viene inizializzato tramite l'esecuzione di [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md), o [DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md) (istruzioni), oppure eseguire qualsiasi routine CLR, tipo o del trigger. Il **sys.dm_clr_properties** vista non specifica se l'esecuzione del codice CLR utente è stata abilitata nel server. L'esecuzione del codice CLR utente viene abilitata tramite il [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) stored procedure con il [clr abilitato](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) opzione impostato su 1.  
  
 Il **sys.dm_clr_properties** vista contiene le **name** e **valore** colonne. Ogni riga della vista include dettagli su una proprietà del CLR hosted. È possibile utilizzare questa vista per raccogliere informazioni sul CLR hosted, ad esempio la directory di installazione di CLR, la versione di CLR e lo stato corrente del CLR hosted. La vista consente inoltre di determinare se il codice dell'integrazione con CLR non funziona a causa di problemi relativi all'installazione di CLR nel computer server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Nome della proprietà.|  
|**Valore**|**nvarchar(128)**|Valore della proprietà.|  
  
## <a name="properties"></a>Proprietà  
 Il **directory** proprietà indica la directory di .NET Framework è stato installato nel server. Nel computer server possono essere presenti più installazioni di .NET Framework. Il valore di questa proprietà identifica l'installazione utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Il **versione** proprietà indica la versione di .NET Framework e del CLR hosted nel server.  
  
 Il **sys.dm_clr_properties** vista a gestione dinamica può restituire sei diversi valori per il **stato** proprietà, che riflette lo stato del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR hosted. Sono:  
  
-   Mscoree is not loaded.  
  
-   Mscoree is loaded.  
  
-   Locked CLR version with mscoree.  
  
-   CLR is initialized.  
  
-   CLR initialization permanently failed.  
  
-   CLR is stopped.  
  
 Il **Mscoree non viene caricata** e **Mscoree viene caricato** stati indicano l'avanzamento dell'inizializzazione del CLR hosted all'avvio del server e non sono soggette a essere visualizzato.  
  
 Il **versione di CLR bloccato con mscoree** stato può essere visualizzato in cui il CLR hosted non è in uso e, di conseguenza, non è ancora stato inizializzato. Il CLR hosted viene inizializzato alla prima esecuzione di un'istruzione DDL (ad esempio [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) o un oggetto di database gestito viene eseguito.  
  
 Il **CLR viene inizializzato** stato indica che il CLR hosted è stato inizializzato correttamente. Si noti che questo stato non indica se l'esecuzione del codice CLR utente è stata abilitata. Se l'esecuzione del codice CLR utente viene prima abilitata e quindi disabilitata utilizzando la [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) stored procedure, il valore di stato ancora verrà **CLR viene inizializzato**.  
  
 Il **inizializzazione di CLR in modo permanente non è stato possibile** stato indica che CLR hosted inizializzazione non riuscita. Le possibili cause sono la scarsa disponibilità di memoria o un errore nell'handshake host tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il CLR. In questo caso verrà generato il messaggio di errore 6512 o 6513.  
  
 Il **CLR viene arrestato lo stato** viene visualizzato solo se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in corso la chiusura.  
  
## <a name="remarks"></a>Note  
 Le proprietà e valori di questa vista potrebbero cambiare nelle versioni future di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a causa di miglioramenti della funzionalità di integrazione CLR.  
  
## <a name="permissions"></a>Permissions  
  
Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione nel database. Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard e i livelli Basic, è necessario il **amministratore del Server** o un' **amministratore di Azure Active Directory** account.   

## <a name="examples"></a>Esempi  
 L'esempio seguente recupera informazioni relative al CLR hosted:  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative a Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
