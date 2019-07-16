---
title: sp_pdw_add_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: da1ba0db4467526ef2b54650020a899f88788648
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008951"
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Consente di archiviare le credenziali di rete in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e li associa a un server. Ad esempio, utilizzare questa stored procedure per offrire [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] appropriate autorizzazioni di lettura/scrittura per eseguire backup del database e le operazioni in un server di destinazione di ripristino o per creare un backup di un certificato usato per TDE.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>Argomenti  
 '*target_server_name*'  
 Specifica il nome host del server di destinazione o indirizzo IP. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] accederà questo server usando le credenziali nome utente e password passate a questa stored procedure.  
  
 Per connettersi tramite la rete InfiniBand, usare l'indirizzo IP InfiniBand del server di destinazione.  
  
 *target_server_name* viene definito come nvarchar(337).  
  
 '*user_name*'  
 Specifica la funzione user_name che dispone delle autorizzazioni per accedere al server di destinazione. Se esistono già credenziali per il server di destinazione, questi verranno aggiornati per le nuove credenziali.  
  
 *USER_NAME* viene definito come nvarchar (513).  
  
 '*password*ꞌ  
 Specifica la password per *user_name*.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 È necessario **ALTER SERVER STATE** l'autorizzazione.  
  
## <a name="error-handling"></a>Gestione degli errori  
 Si verifica un errore se aggiungere le credenziali non riesce nel nodo di controllo e tutti i nodi di calcolo.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Questa stored procedure consente di aggiungere le credenziali di rete per l'account NetworkService per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. L'account NetworkService esegue ogni istanza di SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul nodo di controllo e i nodi di calcolo. Ad esempio, quando viene eseguita un'operazione di backup, il nodo di controllo e ogni nodo di calcolo useranno le credenziali dell'account NetworkService per ottenere in lettura e l'autorizzazione di scrittura per il server di destinazione.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>R. Aggiungere le credenziali per l'esecuzione di un backup del database  
 L'esempio seguente associa le credenziali nome utente e password per il seattle\david utente di dominio con un server di destinazione che abbia un indirizzo IP di 10.172.63.255. Seattle\david l'utente disponga delle autorizzazioni di lettura/scrittura per il server di destinazione. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] memorizza queste credenziali e usarli per leggere e scrivere da e verso il server di destinazione, in base alle esigenze per il backup e le operazioni di ripristino.  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 Il comando di backup richiede che il nome del server deve essere immesso come un indirizzo IP.  
  
> [!NOTE]  
>  Per eseguire il backup del database su InfiniBand, assicurarsi di usare l'indirizzo IP InfiniBand del server di backup.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

