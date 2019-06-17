---
title: Database tempdb - Parallel Data Warehouse | Microsoft Docs
description: Database tempdb in Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63156967"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>database tempdb in Parallel Data Warehouse
**tempdb** è un database di sistema di SQL Server PDW che archivia le tabelle temporanee locali per i database utente. Le tabelle temporanee vengono spesso utilizzate per migliorare le prestazioni delle query. Ad esempio, è possibile usare una tabella temporanea per modularizzare uno script e il riutilizzo dei dati calcolati.  
  
Per altre informazioni sui database di sistema, vedere [database di sistema](system-databases.md).  
  
## <a name="Basics"></a>Concetti e termini chiave  
*tabella temporanea locale*  
Oggetto *tabelle temporanee locali* Usa il prefisso & prima il nome della tabella ed è una tabella temporanea creata da una sessione utente locale. In ogni sessione è possibile accedere solo i dati in tabelle temporanee locali per la propria sessione.  
  
Ogni sessione è possibile visualizzare i metadati delle tabelle temporanee locali in tutte le sessioni. Ad esempio, tutte le sessioni possono visualizzare i metadati per tutte le tabelle temporanee locali con il `SELECT * FROM tempdb.sys.tables` query.  
  
tabella temporanea globale  
*Tabelle temporanee globali*, supportato in SQL Server con il # # sintassi, non sono supportati in questa versione di SQL Server PDW.  
  
pdwtempdb  
**pdwtempdb** è il database che archivia le tabelle temporanee locali.  
  
Non implementa le tabelle temporanee tramite SQL Server PDW**tempdb** database. Al contrario, PDW li archivia in un database denominato pdwtempdb. Questo database esiste in ogni nodo di calcolo ed è invisibile all'utente tramite le interfacce PDW. Nella Console di amministrazione, nella pagina dell'archiviazione, si vedranno questi contabilizzato per in un database di sistema PDW denominato **tempdb sql**.  
  
tempdb  
**tempdb** è il database tempdb di SQL Server. Usa la registrazione minima. SQL Server Usa tempdb nei nodi di calcolo per archiviare le tabelle temporanee necessarie nel corso dell'esecuzione di operazioni di SQL Server.  
  
SQL Server PDW Elimina tabelle da **tempdb** quando:  
  
-   Viene eseguita l'istruzione DROP TABLE.  
  
-   Una sessione viene disconnessa. Vengono eliminate solo le tabelle temporanee per la sessione.  
  
-   L'appliance viene arrestato.  
  
-   Il nodo di controllo dispone di un cluster di failover.  
  
## <a name="general-remarks"></a>Osservazioni generali  
SQL Server PDW esegue le stesse operazioni su tabelle temporanee e tabelle permanenti, a meno che diversamente in modo esplicito. Ad esempio, i dati in tabelle temporanee locali, come tabelle permanenti, distribuiti o replicati tra i nodi di calcolo.  
  
## <a name="LimitationsRestrictions"></a>Limitazioni e restrizioni  
Limitazioni e restrizioni in SQL Server PDW**tempdb** database. Si *non è possibile:*  
  
-   Creare una tabella temporanea globale che inizia con # #.  
  
-   Eseguire un backup o ripristino dei **tempdb**.  
  
-   Modificare le autorizzazioni per **tempdb** con il **Concedi**, **DENY**, oppure **revocare** istruzioni.  
  
-   Eseguire **DBCC SHRINKLOG** per **tempdb**tempdb.  
  
-   Eseguire le operazioni DDL **tempdb**. Esistono due eccezioni a questa. Per informazioni dettagliate, vedere il seguente elenco di limitazioni e restrizioni in tabelle temporanee locali.  
  
Limitazioni e restrizioni per le tabelle temporanee locali. Si *non è possibile:*  
  
-   Rinominare una tabella temporanea  
  
-   Creare indici non cluster, viste o le partizioni in una tabella temporanea. **ALTER INDEX** può essere utilizzato per ricompilare un indice cluster per una tabella creata con uno.  
  
-   Modificare le autorizzazioni per le tabelle temporanee con l'istruzione GRANT, DENY o revocare le istruzioni.  
  
-   Eseguire i comandi della console database nelle tabelle temporanee.  
  
-   Usare lo stesso nome per due o più tabelle temporanee all'interno dello stesso batch. Se si usa più di una tabella temporanea locale all'interno di un batch, ogni tabella deve avere un nome univoco. Se più sessioni eseguono lo stesso batch e creare la stessa tabella temporanea locale, SQL Server PDW aggiunge internamente un suffisso numerico al nome della tabella temporanea locale per gestire un nome univoco per ogni tabella temporanea locale.  
  
> [!NOTE]  
> Si *può* creare e aggiornare le statistiche in una tabella temporanea. **ALTER INDEX** può essere usata per ricompilare un indice cluster.  
  
## <a name="permissions"></a>Permissions  
Qualsiasi utente può creare oggetti temporanei in tempdb. Gli utenti possono accedere solo ai propri oggetti, a meno che non ottengano ulteriori autorizzazioni. È possibile revocare l'autorizzazione per la connessione a tempdb per impedire a un utente di utilizzarlo, tuttavia questa operazione non è consigliabile poiché in alcune operazioni di routine è richiesto l'utilizzo di tempdb.  
  
## <a name="RelatedTasks"></a>Attività correlate  
  
|Attività|Descrizione|  
|---------|---------------|  
|Creare una tabella nel **tempdb**.|È possibile creare una tabella temporanea di utente con le istruzioni CREATE TABLE e CREATE TABLE AS SELECT. Per altre informazioni, vedere [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) e [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Visualizzare un elenco delle tabelle esistenti in **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Visualizzare un elenco di colonne esistenti nella **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Visualizzare un elenco di oggetti esistenti **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
