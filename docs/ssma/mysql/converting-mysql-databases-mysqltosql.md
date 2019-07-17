---
title: Conversione dei database MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1ad4cbbdf80422f87c850c44e47f82899de4c82a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103053"
---
# <a name="converting-mysql-databases-mysqltosql"></a>Conversione di database MySQL (MySQLToSQL)
Dopo essersi connessi a MySQL, connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure e impostare il progetto e opzioni di mapping dei dati, è possibile convertire gli oggetti di database MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o oggetti di database di SQL Azure.  
  
## <a name="the-conversion-process"></a>Il processo di conversione  
Conversione di oggetti di database richiede le definizioni degli oggetti da MySQL, li converte in simile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure o gli oggetti e quindi carica tali informazioni nei metadati di SSMA. Non lo carica le informazioni nell'istanza della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È quindi possibile visualizzare gli oggetti e le relative proprietà utilizzando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure.  
  
Durante la conversione SSMA consente di stampare i messaggi di output nel riquadro di Output e messaggi di errore nel riquadro elenco errori. Usare le informazioni di errore e di output per determinare se è necessario modificare i database di MySQL o il processo di conversione per ottenere i risultati di conversione desiderato.  
  
## <a name="setting-conversion-options"></a>Impostazione delle opzioni di conversione  
Prima di convertire gli oggetti, esaminare le opzioni di conversione progetto nel **impostazioni del progetto** nella finestra di dialogo. Tramite questa finestra di dialogo, è possibile impostare la modalità di conversione di tabelle e indici in SSMA. Per altre informazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Risultati conversione  
La tabella seguente mostra che MySQL gli oggetti vengono convertiti e risultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti:  
  
|||  
|-|-|  
|**Oggetti di MySQL**|**Oggetti SQL Server risultanti**|  
|Tabelle con gli oggetti dipendenti, ad esempio gli indici|SSMA consente di creare tabelle con gli oggetti dipendenti. Nella tabella viene convertita con tutti gli indici e vincoli. Gli indici vengono convertiti in separato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti.<br /><br />**Mapping dei tipi di dati spaziali** può essere eseguita solo a livello di nodo di tabella.<br /><br />Per altre informazioni sulle impostazioni di conversione della tabella, vedere [le impostazioni di conversione](conversion-settings-mysqltosql.md)|  
|Funzioni|Se la funzione può essere convertita direttamente in Transact-SQL, SSMA consente di creare una funzione. In alcuni casi, la funzione deve essere convertita in una stored procedure. Questa operazione può essere eseguita tramite **funzione di conversione** nelle impostazioni del progetto. In questo caso, SSMA consente di creare una stored procedure e una funzione che chiama la stored procedure.<br /><br />**Digitare un valore:**<br /><br />Convertire in base alle impostazioni di progetto<br /><br />Converti in (funzione)<br /><br />Convertire in stored procedure<br /><br />Per altre informazioni sulle impostazioni di conversione (funzione), vedere [le impostazioni di conversione](conversion-settings-mysqltosql.md)|  
|Procedure|Se la procedura può essere convertita direttamente in Transact-SQL, SSMA consente di creare una stored procedure. In alcuni casi una stored procedure deve essere chiamata in una transazione autonoma. In questo caso, SSMA consente di creare due stored procedure: una che implementa la procedura e l'altra che viene usata per chiamare l'implementazione della stored procedure.|  
|Conversione del database|I database come oggetti di MySQL non vengono convertiti direttamente da SSMA per MySQL. Database MySQL sono trattati più come nomi di schema e tutti i parametri fisici vengono persi durante la conversione. SSMA per MySQL Usa [Mapping di database MySQL a schemi SQL Server &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) eseguire il mapping di oggetti da database MySQL-to-pair/schema del database di SQL Server appropriato.|  
|Conversione di trigger|**SSMA consente di creare trigger sulla base delle regole seguenti:**<br /><br />PRIMA che i trigger vengono convertiti nei trigger INSTEAD OF. T-SQL<br /><br />I trigger AFTER vengono convertiti in trigger dopo T-SQL con o senza le iterazioni per le righe.|  
|Conversione di visualizzazione|SSMA consente di creare visualizzazioni con gli oggetti dipendenti|  
|Conversione di istruzioni|-Ogni oggetto istruzione SQL può contenere una singola istruzione di MySQL (ad esempio DDL, DML e altri tipi di istruzioni) o BEGIN... Blocco finale.<br />-   **Conversione con istruzioni multiple: BEGIN... Conversione di fine blocco**istruzione SQL può contenere anche un blocco BEGIN... Blocco di fine, ad esempio una nella definizione di procedure, funzioni o trigger. Tali blocchi devono essere convertiti allo stesso modo che vengono convertite per gli oggetti di istruzione singoli di MySQL.|  
  
## <a name="converting-mysql-database-objects"></a>Conversione di oggetti di Database MySQL  
Per convertire gli oggetti di database MySQL, prima di tutto selezionare gli oggetti che si desidera convertire e quindi SSMA eseguire la conversione. Per visualizzare i messaggi di output durante la conversione nel **View** dal menu **Output**.  
  
**Per convertire gli oggetti di MySQL in sintassi SQL Server o SQL Azure**  
  
1.  Nel Visualizzatore metadati di MySQL, espandere il server MySQL e infine **database**.  
  
2.  Selezionare gli oggetti da convertire:  
  
    -   Per convertire tutti gli schemi, selezionare la casella di controllo accanto a **database**.  
  
    -   Per convertire o omettere un database, selezionare la casella di controllo accanto al nome del Database.  
  
    -   Per convertire o omettere una categoria di oggetti, espandere uno schema, quindi selezionare o deselezionare la casella di controllo accanto alla categoria.  
  
    -   Per convertire o omettere singoli oggetti, espandere la cartella di categoria, quindi selezionare o deselezionare la casella di controllo accanto all'oggetto.  
  
3.  Per convertire tutti gli oggetti selezionati, fare doppio clic su **database** e selezionare **Converti Schema**.  
  
    È anche possibile convertire gli oggetti singoli o categorie di oggetti pulsante destro del mouse relativa cartella padre o l'oggetto e quindi selezionando **convertire lo Schema**.  
  
## <a name="viewing-conversion-problems"></a>Visualizzazione dei problemi di conversione  
Alcuni oggetti di MySQL potrebbero non essere convertiti. È possibile determinare i tassi di conversione riuscita, visualizzando il report di riepilogo di conversione.  
  
**Per visualizzare un report di riepilogo**  
  
1.  Nel Visualizzatore metadati di MySQL, selezionare **database**.  
  
2.  Nel riquadro di destra, selezionare la **Report** scheda.  
  
    Questo report mostra il report di riepilogo di valutazione per tutti gli oggetti di database che sono state valutate o convertiti. È anche possibile visualizzare un report di riepilogo per i singoli oggetti:  
  
    -   Per visualizzare il report per un singolo schema, selezionare il database in Visualizzatore metadati MySQL.  
  
    -   Per visualizzare il report per un singolo oggetto, selezionare l'oggetto in Visualizzatore metadati MySQL. Gli oggetti che presentano problemi di conversione hanno un'icona rossa di errore.  
  
Per gli oggetti che non hanno superato la conversione, è possibile visualizzare la sintassi che ha generato l'errore di conversione.  
  
**Per visualizzare i problemi di conversione singoli**  
  
1.  Nel Visualizzatore metadati di MySQL, espandere **database**.  
  
2.  Espandere il database che viene visualizzata un'icona rossa di errore.  
  
3.  Al database, espandere una cartella con un'icona rossa di errore.  
  
4.  Selezionare l'oggetto che ha un'icona rossa di errore.  
  
5.  Nel riquadro di destra, scegliere il **Report** scheda.  
  
6.  In cima il **Report** scheda è riportato un elenco di riepilogo a discesa. Se l'elenco Mostra **statistiche**, modificare la selezione del **origine**.  
  
    SSMA verrà visualizzato il codice sorgente e diversi pulsanti immediatamente sopra il codice.  
  
7.  Scegliere il **problema successivo** pulsante. Si tratta di un'icona rossa di errore con una freccia che punta a destra.  
  
    SSMA verrà evidenziato il codice sorgente problematico prima che trova nell'oggetto corrente.  
  
Per ogni elemento che non può essere convertito, è necessario determinare ciò che si desidera eseguire operazioni con tale oggetto:  
  
-   È possibile modificare l'oggetto nel database di MySQL per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [connessione a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure i metadati Explorer e Visualizzatore metadati di MySQL, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure e la migrazione dei dati da MySQL.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [caricamento di convertire gli oggetti di Database in SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
