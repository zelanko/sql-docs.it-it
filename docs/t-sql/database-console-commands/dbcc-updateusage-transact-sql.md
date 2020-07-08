---
title: DBCC UPDATEUSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
author: pmasl
ms.author: umajay
ms.openlocfilehash: fa1bd6767a81142e115e02d242a54b9715bf78f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643861"
---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Segnala e corregge le imprecisioni relative al conteggio delle pagine e delle righe nelle viste del catalogo. Queste imprecisioni possono causare la restituzione di report sull'utilizzo dello spazio non corretti da parte della stored procedure di sistema sp_spaceused.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>Argomenti  
*database_name* | *database_id* | 0  
Nome o ID del database per cui si desidera segnalare e correggere le statistiche sull'utilizzo dello spazio. Se si specifica 0, viene utilizzato il database corrente. I nomi dei database devono essere conformi alle regole per gli [identificatori](../../relational-databases/databases/database-identifiers.md).  
  
*table_name* | *table_id* | *view_name* | *view_id*  
Nome o ID della tabella o della vista indicizzata per cui si desidera segnalare e correggere le statistiche sull'utilizzo dello spazio. I nomi delle tabelle e delle viste devono essere conformi alle regole per gli identificatori.  
  
*index_id* | *index_name*  
ID o nome dell'indice da utilizzare. Se viene omesso, l'istruzione elabora tutti gli indici della tabella o della vista specificata.  
  
WITH  
Consente di specificare opzioni.  
  
NO_INFOMSGS  
Disattiva tutti i messaggi informativi.  
  
COUNT_ROWS  
Specifica che la colonna row count viene aggiornata in base al numero di righe corrente della tabella o della vista.  
  
## <a name="remarks"></a>Osservazioni  
L'istruzione DBCC UPDATEUSAGE corregge i conteggi delle righe, delle pagine utilizzate, delle pagine riservate, delle pagine foglia e delle pagine di dati per ogni partizione di una tabella o di un indice. Se nelle tabelle di sistema non vengono rilevate imprecisioni, l'istruzione DBCC UPDATEUSAGE non restituisce alcun dato. Se vengono rilevate e corrette alcune imprecisioni e l'opzione WITH NO_INFOMSGS non è stata utilizzata, l'istruzione DBCC UPDATEUSAGE restituisce le righe e le colonne aggiornate nelle tabelle di sistema.
  
DBCC CHECKDB è stato migliorato in modo da rilevare i casi in cui il conteggio delle pagine o delle righe diventa negativo. In tali situazioni, l'output DBCC CHECKDB include un avviso e l'indicazione di eseguire DBCC UPDATEUSAGE per risolvere il problema.
  
## <a name="best-practices"></a>Procedure consigliate  
È consigliabile attenersi alle linee guida seguenti:
-   Non eseguire regolarmente DBCC UPDATEUSAGE. Poiché l'istruzione DBCC UPDATEUSAGE può richiedere una certa quantità di tempo se eseguita in tabelle o database di grandi dimensioni, deve essere utilizzata solo se si ritiene che valori non corretti vengano restituiti da sp_spaceused.
-   Prevedere un'esecuzione regolare di DBCC UPDATEUSAGE, ad esempio ogni settimana, solo se il database subisce frequenti modifiche DDL (Data Definition Language), come l'istruzione CREATE, ALTER o DROP.  
  
## <a name="result-sets"></a>Set di risultati  
DBCC UPDATEUSAGE restituisce il messaggio seguente (i valori possono variare):
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o al ruolo predefinito del database **db_owner** .
  
## <a name="examples"></a>Esempi  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>R. Aggiornamento del conteggio delle pagine, delle righe o di entrambi per tutti gli oggetti nel database corrente  
Nell'esempio seguente viene specificato il valore `0` per il nome del database e l'istruzione `DBCC UPDATEUSAGE` restituisce informazioni aggiornate relative al conteggio delle pagine o delle righe per il database corrente.
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. Aggiornamento del conteggio delle pagine, delle righe o di entrambi per il database AdventureWorks e disattivazione dei messaggi informativi  
Nell'esempio seguente viene specificato [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] come nome del database e vengono disattivati tutti i messaggi informativi.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. Aggiornamento del conteggio delle pagine, delle righe o di entrambi per la tabella Employee  
Nell'esempio seguente vengono restituite informazioni aggiornate relative al conteggio delle pagine o delle righe per la tabella `Employee` nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. Aggiornamento del conteggio delle pagine, delle righe o di entrambi per un indice specifico di una tabella  
 Nell'esempio seguente viene specificato il valore `IX_Employee_ManagerID` come nome dell'indice.  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  
