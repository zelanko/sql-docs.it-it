---
title: Opzioni (esecuzione Query-SQL Server-ANSI pagina) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e075de106a66ffee63c02ead06a3fc68548111a8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089375"
---
# <a name="options-query-execution-sql-server-ansi-page"></a>Opzioni (esecuzione Query-SQL Server-ANSI pagina)
  L'insieme di queste opzioni SET dello standard ANSI (ISO) definisce l'ambiente di elaborazione della query per l'intera durata della query dell'utente o dell'esecuzione di un trigger o di una stored procedure. Queste opzioni SET tuttavia non includono tutte le opzioni necessarie per la conformità allo standard ISO. Questa pagina consente di indicare se [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debba eseguire le query utilizzando tutte o una parte delle impostazioni specificate nello standard ISO. Le modifiche apportate a queste opzioni vengono applicate solo alle nuove query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per modificare le opzioni relative alle query correnti, scegliere **Opzioni query** dal menu **Query** oppure fare clic con il pulsante destro del mouse nella finestra Query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e quindi scegliere **Opzioni query**. Nella finestra di dialogo **Opzioni query** fare clic su **ANSI**in **Esecuzione**.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **SET ANSI_DEFAULTS**  
 Selezionare questa casella di controllo per selezionare tutte le impostazioni predefinite di ISO. Non tutte le opzioni di ISO sono selezionate per impostazione predefinita.  
  
 **SET QUOTED_IDENTIFIER**  
 Quando questa casella di controllo è selezionata, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] segue le regole ISO relative alle virgolette che delimitano gli identificatori e le stringhe letterali. Gli identificatori delimitati da virgolette possono essere parole chiave riservate di Transact-SQL e possono includere caratteri in genere non consentiti in base alle regole di sintassi per gli identificatori di Transact-SQL. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET ANSI_NULL_DFLT_ON**  
 Se questo valore è impostato, tutti i tipi di dati definiti dall'utente o le colonne non definite esplicitamente come NOT NULL da un'istruzione CREATE TABLE o ALTER TABLE verranno impostati in modo da consentire i valori Null. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 Quando questa casella di controllo è selezionata, SET IMPLICIT_TRANSACTIONS imposta la connessione sulla modalità di esecuzione implicita delle transazioni. Quando questa casella di controllo è deselezionata, viene ripristinata la modalità di transazione con autocommit per la connessione. Per esaminare le istruzioni che avviano una transazione implicita quando vengono selezionate, vedere [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-implicit-transactions-transact-sql). Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 Quando questa casella di controllo è selezionata, tutti i cursori aperti vengono chiusi automaticamente (in conformità allo standard ISO) quando viene eseguito il commit di una transazione. Quando questo valore è impostato su OFF, i cursori rimangono aperti durante la transazione e vengono chiusi soltanto quando la connessione viene chiusa o quando vengono chiusi esplicitamente. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET ANSI_PADDING**  
 Controlla il modo in cui la colonna archivia i nomi di valore inferiori alle dimensioni definite della colonna e il modo in cui memorizza valori contenenti spazi vuoti finali nei dati **char**, **varchar**, **binary**e **varbinary** . Questa impostazione influisce solo sulla definizione di nuove colonne. Dopo la creazione della colonna, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] archivia i valori in base all'impostazione specificata in fase di creazione. Le successive modifiche dell'impostazione non influiscono sulle colonne esistenti. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET ANSI_WARNINGS**  
 Specifica il funzionamento standard ISO in varie condizioni di errore.  
  
-   Se questa casella di controllo è selezionata e le funzioni di aggregazione, ad esempio SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP o COUNT, includono valori Null, viene generato un messaggio di avviso. Quando è impostata su OFF, non viene visualizzato alcun messaggio di avviso.  
  
-   Quando questa casella di controllo è deselezionata, in seguito a errori di divisione per zero e di overflow aritmetico viene eseguito il rollback dell'istruzione e viene visualizzato un messaggio di errore. Quando è impostata su OFF, a seguito di errori di divisione per zero e di overflow aritmetico vengono restituiti valori Null. Si verifica un errore di divisione per zero o di overflow aritmetico se viene eseguita un'operazione INSERT o UPDATE in una colonna di tipo **character**, **Unicode** o **binary** in cui la lunghezza di un nuovo valore supera le dimensioni massime della colonna. Se l'opzione SET ANSI_WARNINGS è impostata su ON, l'operazione INSERT o UPDATE viene annullata, come specificato dallo standard ISO. Nelle colonne di tipo carattere vengono ignorati gli spazi finali, mentre nelle colonne binarie vengono ignorati i valori Null finali. Quando l'opzione è impostata su OFF, i dati vengono troncati in base alle dimensioni della colonna e l'istruzione ha esito positivo.  
  
 Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET ANSI_NULLS**  
 -   Consente di specificare il funzionamento conforme allo standard ISO degli operatori di confronto uguale a (=) e diverso da (<>) quando questi vengono utilizzati con valori Null. Quando SET ANSI_NULLS è selezionata, tutti i confronti con un valore Null restituiscono UNKNOWN, in conformità allo standard ISO. Quando SET ANSI_NULLS non è selezionata, i confronti di tutti i dati con un valore Null restituiscono TRUE. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **Ripristina predefiniti**  
 Reimposta le impostazioni predefinite originali per tutti i valori nella pagina.  
  
  
