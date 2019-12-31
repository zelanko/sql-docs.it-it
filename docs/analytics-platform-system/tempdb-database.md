---
title: Database tempdb
description: Database tempdb in parallelo data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3772e2b4cabac84c00854eba85f7a0c2a33d48bc
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400144"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>database tempdb in parallelo data warehouse
**tempdb** è un database di sistema SQL Server PDW che archivia le tabelle temporanee locali per i database utente. Le tabelle temporanee vengono spesso utilizzate per migliorare le prestazioni di esecuzione delle query. Ad esempio, è possibile usare una tabella temporanea per modularizzare uno script e riusare i dati calcolati.  
  
Per ulteriori informazioni sui database di sistema, vedere [database di sistema](system-databases.md).  
  
## <a name="Basics"></a>Termini e concetti chiave  
*tabella temporanea locale*  
Una *tabella temporanea locale* usa il prefisso # prima del nome della tabella ed è una tabella temporanea creata da una sessione utente locale. Ogni sessione può accedere solo ai dati nelle tabelle temporanee locali per la propria sessione.  
  
Ogni sessione può visualizzare i metadati per le tabelle temporanee locali in tutte le sessioni. Tutte le sessioni, ad esempio, possono visualizzare i metadati per tutte le tabelle temporanee locali con la `SELECT * FROM tempdb.sys.tables` query.  
  
tabella temporanea globale  
Le *tabelle temporanee globali*, supportate in SQL Server con la sintassi # #, non sono supportate in questa versione di SQL Server PDW.  
  
pdwtempdb  
**pdwtempdb** è il database in cui sono archiviate le tabelle temporanee locali.  
  
PDW non implementa le tabelle temporanee tramite il SQL Server database**tempdb** . Al contrario, PDW li archivia in un database denominato pdwtempdb. Questo database esiste in ogni nodo di calcolo ed è invisibile all'utente tramite le interfacce PDW. Nella pagina archiviazione della console di amministrazione si vedranno questi account in un database di sistema PDW denominato **tempdb-SQL**.  
  
tempdb  
**tempdb** è il SQL Server database tempdb. Usa la registrazione minima. SQL Server usa tempdb nei nodi di calcolo per archiviare le tabelle temporanee necessarie nel corso dell'esecuzione di SQL Server operazioni.  
  
SQL Server PDW Elimina le tabelle da **tempdb** nei casi seguenti:  
  
-   L'istruzione DROP TABLE viene eseguita.  
  
-   Una sessione è disconnessa. Vengono eliminate solo le tabelle temporanee per la sessione.  
  
-   L'appliance è stata arrestata.  
  
-   Il nodo di controllo ha un failover del cluster.  
  
## <a name="general-remarks"></a>Osservazioni generali  
SQL Server PDW esegue le stesse operazioni sulle tabelle temporanee e sulle tabelle permanenti se non diversamente specificato in modo esplicito. Ad esempio, i dati in tabelle temporanee locali, analogamente alle tabelle permanenti, vengono distribuiti o replicati nei nodi di calcolo.  
  
## <a name="LimitationsRestrictions"></a>Limitazioni e restrizioni  
Limitazioni e restrizioni relative al database di SQL Server PDW**tempdb** . *Non è possibile:*  
  
-   Creare una tabella temporanea globale che inizia con # #.  
  
-   Eseguire un backup o un ripristino di **tempdb**.  
  
-   Modificare le autorizzazioni per **tempdb** con le istruzioni **Grant**, **Deny**o **Revoke** .  
  
-   Eseguire **DBCC SHRINKLOG** per **tempdb tempdb.**  
  
-   Eseguire operazioni DDL su **tempdb**. Sono presenti due eccezioni. Per informazioni dettagliate, vedere l'elenco seguente di limitazioni e restrizioni sulle tabelle temporanee locali.  
  
Limitazioni e restrizioni sulle tabelle temporanee locali. *Non è possibile:*  
  
-   Rinominare una tabella temporanea  
  
-   Creazione di partizioni, viste o indici non cluster in una tabella temporanea. È possibile utilizzare **alter index** per ricompilare un indice cluster per una tabella creata con una tabella.  
  
-   Modificare le autorizzazioni per le tabelle temporanee con le istruzioni GRANT, DENY o REVOKE.  
  
-   Eseguire i comandi della console di database nelle tabelle temporanee.  
  
-   Usare lo stesso nome per due o più tabelle temporanee all'interno dello stesso batch. Se si usa più di una tabella temporanea locale all'interno di un batch, ogni tabella deve avere un nome univoco. Se più sessioni eseguono lo stesso batch e creano la stessa tabella temporanea locale, SQL Server PDW aggiunge internamente un suffisso numerico al nome della tabella temporanea locale per mantenere un nome univoco per ogni tabella temporanea locale.  
  
> [!NOTE]  
> È *possibile* creare e aggiornare le statistiche in una tabella temporanea. È possibile utilizzare **alter index** per ricompilare un indice cluster.  
  
## <a name="permissions"></a>Autorizzazioni  
Qualsiasi utente può creare oggetti temporanei in tempdb. Gli utenti possono accedere solo ai propri oggetti, a meno che non ottengano ulteriori autorizzazioni. È possibile revocare l'autorizzazione per la connessione a tempdb per impedire a un utente di utilizzarlo, tuttavia questa operazione non è consigliabile poiché in alcune operazioni di routine è richiesto l'utilizzo di tempdb.  
  
## <a name="RelatedTasks"></a>Attività correlate  
  
|Attività|Description|  
|---------|---------------|  
|Creare una tabella in **tempdb**.|È possibile creare una tabella temporanea dell'utente con il CREATE TABLE e CREATE TABLE come istruzioni SELECT. Per ulteriori informazioni, vedere [Create Table](../t-sql/statements/create-table-azure-sql-data-warehouse.md) e [create table come SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md).|  
|Visualizzazione di un elenco di tabelle esistenti in **tempdb**.|`SELECT * FROM tempdb.sys.tables;`|  
|Visualizzazione di un elenco di colonne esistenti in **tempdb**.|`SELECT * FROM tempdb.sys.columns;`|  
|Visualizzazione di un elenco di oggetti esistenti in **tempdb**.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
