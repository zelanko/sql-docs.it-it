---
description: sp_pdw_remove_network_credentials (SQL Data Warehouse)
title: sp_pdw_remove_network_credentials
titleSuffix: Azure SQL Data Warehouse
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
ms.custom: seo-dt-2019
ms.openlocfilehash: 548779915a1d3a1753a99b16ac95969c755cbb19
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988777"
---
# <a name="sp_pdw_remove_network_credentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (SQL Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Questa operazione rimuove le credenziali di rete archiviate in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] per accedere a una condivisione file di rete. Usare, ad esempio, questo stored procedure per rimuovere l'autorizzazione per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] l'esecuzione di operazioni di backup e ripristino in un server che risiede nella propria rete.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>Argomenti  
 '*target_server_name*'  
 Specifica il nome host o l'indirizzo IP del server di destinazione. Le credenziali per accedere a questo server verranno rimosse da [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . Questa operazione non comporta la modifica o la rimozione delle autorizzazioni per il server di destinazione effettivo gestito dal team.  
  
 *target_server_name* è definito come nvarchar (337).  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione **ALTER server state** .  
  
## <a name="error-handling"></a>Gestione degli errori  
 Si verifica un errore se la rimozione delle credenziali non riesce nel nodo di controllo e in tutti i nodi di calcolo.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Questa stored procedure rimuove le credenziali di rete dall'account NetworkService per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . L'account NetworkService esegue ogni istanza di SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul nodo di controllo e sui nodi di calcolo. Ad esempio, quando viene eseguita un'operazione di backup, il nodo di controllo e ogni nodo di calcolo utilizzeranno le credenziali dell'account NetworkService per accedere al server di destinazione.  
  
## <a name="metadata"></a>Metadati  
 Per elencare tutte le credenziali e per verificare che le credenziali siano state rimosse, utilizzare [sys.dm_pdw_network_credentials &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Per aggiungere le credenziali, usare [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>R. Rimuovere le credenziali per l'esecuzione di un backup del database  
 Nell'esempio seguente vengono rimosse le credenziali del nome utente e della password per l'accesso al server di destinazione con un indirizzo IP di 10.192.147.63.  
  
```sql  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

