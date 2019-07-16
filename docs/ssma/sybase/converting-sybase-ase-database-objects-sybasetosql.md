---
title: Conversione di oggetti di Database di ASE Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 507ac2a61043260435a18c90fb473130988e7f35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948519"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>Conversione di oggetti di database SAP ASE (SybaseToSQL)
Dopo essersi connessi a SAP Adaptive Server Enterprise (ASE), connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL di Azure e impostare il progetto e opzioni di mapping dei dati, è possibile convertire gli oggetti di database SAP Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure oggetti.  
  
## <a name="the-conversion-process"></a>Il processo di conversione  
Conversione di oggetti di database richiede le definizioni degli oggetti dall'ambiente del servizio App, li converte in simile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure o gli oggetti e quindi carica tali informazioni nei metadati di SSMA. Non lo carica le informazioni nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL di Azure. È quindi possibile visualizzare gli oggetti e le relative proprietà utilizzando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati SQL di Azure.
  
Durante la conversione SSMA Stampa messaggi di output per i messaggi di errore e riquadro di Output per il **elenco errori** riquadro. Usare le informazioni di errore e di output per determinare se è necessario modificare i database ambiente del servizio App o il processo di conversione per ottenere i risultati di conversione desiderato.  
  
## <a name="setting-conversion-options"></a>Impostazione delle opzioni di conversione  
Prima di convertire gli oggetti, esaminare le opzioni di conversione progetto nel **impostazioni del progetto** nella finestra di dialogo. Tramite questa finestra di dialogo, è possibile impostare la modalità di conversione di funzioni e variabili globali in SSMA. Per altre informazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Conversione di oggetti di database ambiente del servizio App  
Per convertire gli oggetti di database di ambiente del servizio App, selezionare innanzitutto gli oggetti che si desidera convertire e hanno quindi SSMA eseguire la conversione. Per visualizzare i messaggi di output durante la conversione nel **View** dal menu **Output**.  
  
**Per convertire gli oggetti di ambiente del servizio App per la sintassi di SQL Server o SQL Azure**  
  
1.  Nel Visualizzatore metadati Sybase, espandere il server dell'ambiente del servizio App e quindi espandere **database**.  
  
2.  Selezionare gli oggetti da convertire:  
  
    -   Per convertire tutti i database, selezionare la casella di controllo accanto a **database**.  
  
    -   Per convertire o omettere un database, selezionare o deselezionare la casella di controllo accanto al nome del database.  
  
    -   Per convertire o omettere singoli schemi, espandere il database, espandere **schemi**e quindi selezionare o deselezionare la casella di controllo accanto a schema.  
  
    -   Per convertire o omettere una categoria di oggetti, espandere lo schema, quindi selezionare o deselezionare la casella di controllo accanto alla categoria.  
  
    -   Per convertire o omettere singoli oggetti, espandere la cartella di categoria, quindi selezionare o deselezionare la casella di controllo accanto all'oggetto.  
  
3.  Per convertire tutti gli oggetti selezionati, fare doppio clic su **database**, quindi selezionare **Converti Schema**.  
  
    È anche possibile convertire gli oggetti singoli o categorie di oggetti facendo clic su oggetto o la cartella che contiene, e quindi selezionando **convertire lo Schema**.  
  
> [!NOTE]  
> Alcune delle funzioni di sistema SAP ASE non corrispondono esattamente le funzioni di sistema di SQL Server equivalente nel comportamento. Per emulare il comportamento di SAP ASE, SSMA genera le funzioni definite dall'utente nel database di SQL Server convertito in un schema denominato 's2ss'. A seconda delle impostazioni di progetto, alcune delle funzioni di sistema SQL Server vengono sostituite con queste funzioni emulate. SSMA consente di creare le funzioni definite dall'utente seguenti:  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Oggetti non supportati in SQL Azure  
Le parole chiave T-SQL seguenti vengono utilizzate da SSMA per ASE SAP durante la conversione in SQL Server in locale, ma queste parole chiave non sono supportate dalla sintassi T-SQL di SQL Azure:  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>Visualizzazione dei problemi di conversione  
Alcuni oggetti di SAP ASE potrebbero non essere convertito. È possibile determinare i tassi di conversione riuscita, visualizzando il report di riepilogo di conversione.  
  
**Per visualizzare un report di riepilogo**  
  
1.  Nel Visualizzatore metadati Sybase, selezionare **database**.  
  
2.  Nel riquadro di destra, selezionare la **Report** scheda.  
  
    Questo report mostra il report di riepilogo di valutazione per tutti gli oggetti di database che sono state valutate o convertiti. È anche possibile visualizzare un report di riepilogo per i singoli oggetti:  
  
    -   Per visualizzare il report per un singolo database, selezionare il database in Visualizzatore metadati Sybase.  
  
    -   Per visualizzare il report per un oggetto di database singoli, selezionare l'oggetto in Visualizzatore metadati Sybase. Gli oggetti che presentano problemi di conversione hanno un'icona rossa di errore.  
  
Per gli oggetti che non hanno superato la conversione, è possibile visualizzare la sintassi che ha generato l'errore di conversione.  
  
**Per visualizzare i problemi di conversione singoli**  
  
1.  Nel Visualizzatore metadati Sybase, espandere **database**.  
  
2.  Espandere il database che viene visualizzata un'icona rossa di errore.  
  
3.  Espandere la **schemi** cartella, quindi espandere lo schema che mostra un'icona rossa di errore.  
  
4.  Espandere una cartella con un'icona rossa di errore, lo schema.  
  
5.  Selezionare l'oggetto che ha un'icona rossa di errore.  
  
6.  Nel riquadro di destra, selezionare la **Report** scheda.  
  
7.  In cima il **Report** scheda è riportato un elenco di riepilogo a discesa. Se l'elenco Mostra **statistiche**, modificare la selezione del **origine**.  
  
    SSMA verrà visualizzato il codice sorgente e diversi pulsanti immediatamente sopra il codice.  
  
8.  Selezionare **problema successivo**, un'icona rossa di errore con una freccia rivolta verso destra.  
  
    SSMA per ASE SAP verrà evidenziato il codice sorgente problematico prima che trova nell'oggetto corrente.  
  
Per ogni elemento che non può essere convertito, è necessario determinare ciò che si desidera eseguire operazioni con tale oggetto:  
  
-   È possibile modificare il codice sorgente per le procedure e trigger nel **SQL** scheda.  
  
-   È possibile modificare l'oggetto di SAP ASE per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [la connessione a SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL metadati Explorer e Visualizzatore metadati Sybase, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL di Azure e la migrazione dei dati da SAP ASE.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo del processo di migrazione consiste [caricamento di convertire gli oggetti di Database in SQL Server / SQL Azure (SybaseToSQL)](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database SAP ASE a SQL Server - Database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
