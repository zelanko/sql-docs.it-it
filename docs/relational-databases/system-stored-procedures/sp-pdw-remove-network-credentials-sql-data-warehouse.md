---
title: sp_pdw_remove_network_credentials
titleSuffix: Azure SQL Data Warehouse
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.subservice: design
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7068beee49260db17e7b8f704e5aba316deb6ea3
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844444"
---
# <a name="sp_pdw_remove_network_credentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Questa operazione rimuove le credenziali di rete archiviate nel [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] per accedere a una condivisione file di rete. Ad esempio, usare questa stored procedure per rimuovere l'autorizzazione per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] eseguire operazioni di backup e ripristino in un server che risiede all'interno della propria rete.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>Argomenti  
 '*target_server_name*'  
 Specifica il nome host o l'indirizzo IP del server di destinazione. Le credenziali per accedere a questo server verranno rimosse dal [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Questa operazione non comporta la modifica o la rimozione delle autorizzazioni per il server di destinazione effettivo gestito dal team.  
  
 *target_server_name* è definito come nvarchar (337).  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione **ALTER server state** .  
  
## <a name="error-handling"></a>Gestione degli errori  
 Si verifica un errore se la rimozione delle credenziali non riesce nel nodo di controllo e in tutti i nodi di calcolo.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Questo stored procedure rimuove le credenziali di rete dall'account NetworkService per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. L'account NetworkService esegue ogni istanza di SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul nodo di controllo e sui nodi di calcolo. Ad esempio, quando viene eseguita un'operazione di backup, il nodo di controllo e ogni nodo di calcolo utilizzeranno le credenziali dell'account NetworkService per accedere al server di destinazione.  
  
## <a name="metadata"></a>Metadati  
 Per elencare tutte le credenziali e per verificare che le credenziali siano state rimosse, utilizzare [sys &#40;.&#41;dm_pdw_network_credentials Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Per aggiungere le credenziali, [usare &#40;sp_pdw_add_network_credentials&#41;SQL data warehouse](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. Rimuovere le credenziali per l'esecuzione di un backup del database  
 Nell'esempio seguente vengono rimosse le credenziali del nome utente e della password per l'accesso al server di destinazione con un indirizzo IP di 10.192.147.63.  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

