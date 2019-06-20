---
title: Conversione di schemi Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 18da150a435b5d3d61740139309d109a16691da3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288888"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Conversione di schemi Oracle (OracleToSQL)
Dopo aver connesso a Oracle, connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e impostare il progetto e le opzioni di mapping dei dati, è possibile convertire gli oggetti di database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli oggetti di database.  
  
## <a name="the-conversion-process"></a>Il processo di conversione  
Conversione di oggetti di database richiede le definizioni degli oggetti da Oracle, li converte in simile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti e quindi carica tali informazioni nei metadati di SSMA. Non lo carica le informazioni nell'istanza della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È quindi possibile visualizzare gli oggetti e le relative proprietà utilizzando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati.  
  
Durante la conversione SSMA consente di stampare i messaggi di output nel riquadro di Output e messaggi di errore nel riquadro elenco errori. Usare le informazioni di errore e di output per determinare se è necessario modificare i database Oracle o il processo di conversione per ottenere i risultati di conversione desiderato.  
  
## <a name="setting-conversion-options"></a>Impostazione delle opzioni di conversione  
Prima di convertire gli oggetti, esaminare le opzioni di conversione progetto nel **impostazioni del progetto** nella finestra di dialogo. Tramite questa finestra di dialogo, è possibile impostare la modalità di conversione di funzioni e variabili globali in SSMA. Per altre informazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Risultati conversione  
La tabella seguente mostra quali oggetti Oracle vengono convertiti e risultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti:  
  
|||  
|-|-|  
|Oggetti di Oracle|Oggetti SQL Server risultanti|  
|Funzioni|Se la funzione può essere convertita direttamente in [!INCLUDE[tsql](../../includes/tsql-md.md)], SSMA consente di creare una funzione.<br /><br />In alcuni casi, la funzione deve essere convertita in una stored procedure. In questo caso, SSMA consente di creare una stored procedure e una funzione che chiama la stored procedure.|  
|Procedure|Se la procedura può essere convertita direttamente in [!INCLUDE[tsql](../../includes/tsql-md.md)], SSMA consente di creare una stored procedure.<br /><br />In alcuni casi una stored procedure deve essere chiamata in una transazione autonoma. In questo caso, SSMA consente di creare due stored procedure: una che implementa la procedura e l'altra che viene usata per chiamare l'implementazione della stored procedure.|  
|Pacchetti|SSMA consente di creare un set di stored procedure e funzioni che vengono unificate da nomi di oggetti simili.|  
|Sequenze|SSMA consente di creare gli oggetti sequenza (SQL Server 2012 o SQL Server 2014) o emula le sequenze di Oracle.|  
|Tabelle con gli oggetti dipendenti, ad esempio indici e trigger|SSMA consente di creare tabelle con gli oggetti dipendenti.|  
|Consente di visualizzare gli oggetti dipendenti, ad esempio i trigger|SSMA consente di creare visualizzazioni con gli oggetti dipendenti.|  
|Viste materializzate|**SSMA consente di creare viste indicizzate in SQL server con alcune eccezioni. Conversione non riesce se la vista materializzata include uno o più dei costrutti seguenti:**<br /><br />Funzione definita dall'utente<br /><br />Campo non deterministica / funzione / espressione di selezione, in cui le clausole GROUP BY o<br /><br />Utilizzo della colonna Float in SELECT *, dove o clausole GROUP BY (caso speciale di problema precedente)<br /><br />(Tabelle incluse annidati) del tipo di dati personalizzati<br /><br />CONTEGGIO (distinct &lt;campo&gt;)<br /><br />FETCH<br /><br />OUTER join (LEFT, RIGHT o FULL)<br /><br />Sottoquery, altre visualizzazioni<br /><br />OVER, RANK, LEAD, LOG<br /><br />MIN, MAX<br /><br />UNION, MENO (-), SI INTERSECANO<br /><br />HAVING|  
|Trigger|**SSMA consente di creare trigger sulla base delle regole seguenti:**<br /><br />PRIMA che i trigger vengono convertiti in trigger INSTEAD OF.<br /><br />I trigger AFTER vengono convertiti in trigger AFTER.<br /><br />I trigger INSTEAD OF vengono convertiti in trigger INSTEAD OF. Più trigger INSTEAD OF definito nella stessa operazione sono combinati in un trigger.<br /><br />I trigger a livello di riga vengono emulati utilizzano i cursori.<br /><br />Trigger di propagazione vengono convertiti in più trigger singolo.|  
|Sinonimi|**I sinonimi vengono creati per i tipi di oggetti seguenti:**<br /><br />Le tabelle e oggetti<br /><br />Le viste e le viste di oggetti<br /><br />Stored procedure<br /><br />Funzioni<br /><br />**I sinonimi per gli oggetti seguenti sono risolte e sostituiti da riferimenti a oggetti diretti:**<br /><br />Sequenze<br /><br />Pacchetti<br /><br />Oggetti dello schema di classe Java<br /><br />Tipi di oggetto definito dall'utente<br /><br />I sinonimi per un altro sinonimo non possono essere migrati e verranno contrassegnati come errori.<br /><br />I sinonimi non vengono creati per le visualizzazioni Materialized.|  
|Tipi definiti dall'utente|**SSMA è incluso alcun supporto per la conversione dei tipi definiti dall'utente. Tipi definiti dall'utente, incluso il relativo utilizzo in programmi PL/SQL sono contrassegnati con errori di conversione speciale guidati dalle seguenti regole:**<br /><br />Colonna della tabella di un tipo definito dall'utente viene convertita in VARCHAR(8000).<br /><br />Tipo definito dall'argomento dell'utente a una stored procedure o funzione viene convertita in VARCHAR(8000).<br /><br />Variabile di tipo definito dall'utente nel blocco PL/SQL viene convertito in VARCHAR(8000).<br /><br />Tabella degli oggetti viene convertita in una tabella Standard.<br /><br />Vista dell'oggetto viene convertito in una vista Standard.|  
  
## <a name="converting-oracle-database-objects"></a>Conversione di oggetti di Database Oracle  
Per convertire gli oggetti di database Oracle, prima di tutto selezionare gli oggetti che si desidera convertire e quindi SSMA eseguire la conversione. Per visualizzare i messaggi di output durante la conversione nel **View** dal menu **Output**.  
  
**Per convertire oggetti Oracle in sintassi SQL Server**  
  
1.  Nel Visualizzatore metadati Oracle, espandere il server Oracle e quindi espandere **schemi**.  
  
2.  Selezionare gli oggetti da convertire:  
  
    -   Per convertire tutti gli schemi, selezionare la casella di controllo accanto a **schemi**.  
  
    -   Per convertire o omettere un database, selezionare la casella di controllo accanto al nome dello schema.  
  
    -   Per convertire o omettere una categoria di oggetti, espandere uno schema, quindi selezionare o deselezionare la casella di controllo accanto alla categoria.  
  
    -   Per convertire o omettere singoli oggetti, espandere la cartella di categoria, quindi selezionare o deselezionare la casella di controllo accanto all'oggetto.  
  
3.  Per convertire tutti gli oggetti selezionati, fare doppio clic su **schemi** e selezionare **Converti Schema**.  
  
    È anche possibile convertire gli oggetti singoli o categorie di oggetti pulsante destro del mouse relativa cartella padre o l'oggetto e quindi selezionando **convertire lo Schema**.  
  
## <a name="viewing-conversion-problems"></a>Visualizzazione dei problemi di conversione  
Alcuni oggetti Oracle potrebbero non essere convertiti. È possibile determinare i tassi di conversione riuscita, visualizzando il report di riepilogo di conversione.  
  
**Per visualizzare un report di riepilogo**  
  
1.  Nel Visualizzatore metadati Oracle, selezionare **schemi**.  
  
2.  Nel riquadro di destra, selezionare la **Report** scheda.  
  
    Questo report mostra il report di riepilogo di valutazione per tutti gli oggetti di database che sono state valutate o convertiti. È anche possibile visualizzare un report di riepilogo per i singoli oggetti:  
  
    -   Per visualizzare il report per un singolo schema, selezionare lo schema in Visualizzatore metadati Oracle.  
  
    -   Per visualizzare il report per un singolo oggetto, selezionare l'oggetto in Visualizzatore metadati Oracle. Gli oggetti che presentano problemi di conversione hanno un'icona rossa di errore.  
  
Per gli oggetti che non hanno superato la conversione, è possibile visualizzare la sintassi che ha generato l'errore di conversione.  
  
**Per visualizzare i problemi di conversione singoli**  
  
1.  Nel Visualizzatore metadati Oracle, espandere **schemi**.  
  
2.  Espandere lo schema che mostra un'icona rossa di errore.  
  
3.  Espandere una cartella con un'icona rossa di errore, lo schema.  
  
4.  Selezionare l'oggetto che ha un'icona rossa di errore.  
  
5.  Nel riquadro di destra, scegliere il **Report** scheda.  
  
6.  In cima il **Report** scheda è riportato un elenco di riepilogo a discesa. Se l'elenco Mostra **statistiche**, modificare la selezione del **origine**.  
  
    SSMA verrà visualizzato il codice sorgente e diversi pulsanti immediatamente sopra il codice.  
  
7.  Scegliere il **problema successivo** pulsante. Si tratta di un'icona rossa di errore con una freccia che punta a destra.  
  
    SSMA verrà evidenziato il codice sorgente problematico prima che trova nell'oggetto corrente.  
  
Per ogni elemento che non può essere convertito, è necessario determinare ciò che si desidera eseguire operazioni con tale oggetto:  
  
-   È possibile modificare il codice sorgente per le procedure sul **SQL** scheda.  
  
-   È possibile modificare l'oggetto nel database Oracle per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [connessione a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati ed Esplora i metadati di Oracle, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la migrazione dei dati da Oracle.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [caricare gli oggetti convertiti in SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
