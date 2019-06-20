---
title: Conversione di schemi DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d509ad58491bca379e3ab86e07aee63e8a5d3946
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298972"
---
# <a name="converting-db2-schemas-db2tosql"></a>Conversione di schemi DB2 (DB2ToSQL)
Dopo aver connesso a DB2, connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e impostare il progetto e le opzioni di mapping dei dati, è possibile convertire gli oggetti di database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli oggetti di database.  
  
## <a name="the-conversion-process"></a>Il processo di conversione  
Conversione di oggetti di database richiede le definizioni degli oggetti da DB2, li converte in simile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti e quindi carica tali informazioni nei metadati di SSMA. Non lo carica le informazioni nell'istanza della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È quindi possibile visualizzare gli oggetti e le relative proprietà utilizzando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati.  
  
Durante la conversione SSMA consente di stampare i messaggi di output nel riquadro di Output e messaggi di errore nel riquadro elenco errori. Usare le informazioni di errore e di output per determinare se è necessario modificare i database di DB2 o il processo di conversione per ottenere i risultati di conversione desiderato.  
  
## <a name="setting-conversion-options"></a>Impostazione delle opzioni di conversione  
Prima di convertire gli oggetti, esaminare le opzioni di conversione progetto nel **impostazioni del progetto** nella finestra di dialogo. Tramite questa finestra di dialogo, è possibile impostare la modalità di conversione di funzioni e variabili globali in SSMA. Per altre informazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>Risultati conversione  
La tabella seguente mostra quali vengono convertiti in oggetti di DB2 e risultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti:  
  
|Oggetti di DB2|Oggetti SQL Server risultanti|  
|-----------|----------------------------|  
|Tipi di dati|**SSMA esegue il mapping di ogni tipo, ad eccezione di quanto segue elencati di seguito:**<br /><br />TALE OGGETTO: Alcune funzioni native per il lavoro con questo tipo non sono supportati (ad esempio CLOB_EMPTY())<br /><br />BLOB: Alcune funzioni native per il lavoro con questo tipo non sono supportati (ad esempio BLOB_EMPTY())<br /><br />DBLOB: Alcune funzioni native per il lavoro con questo tipo non sono supportati (ad esempio DBLOB_EMPTY())|  
|Tipi definiti dall'utente|**SSMA viene eseguito il mapping seguente definito dall'utente:**<br /><br />Tipo distinto<br /><br />Tipo strutturato<br /><br />Tipi di dati SQL PL - Nota: Tipo di cursore vulnerabili non sono supportati.|  
|Registri speciali|**SSMA esegue il mapping solo registri elencati di seguito:**<br /><br />TIMESTAMP CORRENTE<br /><br />DATA CORRENTE<br /><br />ORA CORRENTE<br /><br />FUSO ORARIO CORRENTE<br /><br />UTENTE CORRENTE<br /><br />SESSION_USER e utente<br /><br />SYSTEM_USER<br /><br />CLIENT_APPLNAME CORRENTE<br /><br />CLIENT_WRKSTNNAME CORRENTE<br /><br />TIMEOUT DEL BLOCCO CORRENTE<br /><br />SCHEMA CORRENTE<br /><br />SERVER CORRENTE<br /><br />ISOLAMENTO CORRENTE<br /><br />Altri registri speciali non sono mappati a SQL server Semantic Model.|  
|CREATE TABLE|**SSMA viene eseguito il mapping CREATE TABLE con le eccezioni seguenti:**<br /><br />Tabelle di clustering (MDC) multidimensionali<br /><br />Tabelle cluster intervallo (RCT)<br /><br />Tabelle partizionate<br /><br />Tabella scollegata<br /><br />Clausola di acquisizione dei dati<br /><br />Opzione IMPLICITLY NASCOSTE<br /><br />Opzione VOLATILE|  
|CREATE VIEW|SSMA viene eseguito il mapping CREATE VIEW con 'WITH locale CHECK OPTION', ma le altre opzioni non sono mappati alla semantica SQL server|  
|CREATE INDEX|**SSMA viene eseguito il mapping CREATE INDEX con le eccezioni seguenti:**<br /><br />Indice XML<br /><br />Opzione BUSINESS_TIME senza SOVRAPPOSIZIONI<br /><br />Clausola PARTIZIONATA<br /><br />Specifica solo opzione<br /><br />Estendi utilizzo della clausola option<br /><br />Opzione MINPCTUSED<br /><br />Opzione di divisione pagina|  
|Trigger|**SSMA è mappata la semantica di trigger seguenti:**<br /><br />Dopo aver / per ogni riga trigger<br /><br />Dopo aver /FOR ogni istruzione attiva<br /><br />PRIMA di / per ogni riga e INVECE di / per ogni riga trigger|  
|Sequenze|Viene eseguito il mapping.|  
|Istruzione SELECT|**Mappe SSMA selezionato con le eccezioni seguenti:**<br /><br />Clausola di dati-Modifica-tabella-reference - parzialmente eseguito il mapping, ma tabelle finale viene non è supportato<br /><br />Clausola di riferimento alla tabella: parzialmente il mapping, ma solo-tabella-reference, outer-tabella-reference, analyze_table-expression, tabella derivata collection, xmltable-espressioni non sono mappati alla semantica SQL server<br /><br />Specifica del periodo di clausola: non è mappata.<br /><br />Clausola del gestore continuare - non mappata.<br /><br />Clausola di correlazione tipizzata - non mappata.<br /><br />Clausola Concurrent-accesso-resolution - non mappata.|  
|Istruzione di valori|Viene eseguito il mapping.|  
|INSERT-istruzione|Viene eseguito il mapping.|  
|Istruzione UPDATE|S**SMA esegue il mapping di aggiornamento con le eccezioni seguenti:**<br /><br />Riferimento alla tabella clausola - Only-tabella-riferimenti non è mappata a una semantica SQL server<br /><br />Clausola periodo: non è mappata.|  
|Istruzione MERGE|**SSMA esegue il mapping di tipo MERGE con le eccezioni seguenti:**<br /><br />Visual Studio più occorrenze di ogni clausola Single - viene eseguito il mapping alla semantica SQL server limitata occorrenze di ogni clausola<br /><br />Clausola di segnale: non è mappato a una semantica di SQL Server<br /><br />Modalità mista aggiornamento e le clausole DELETE - non esegue il mapping alla semantica di SQL Server<br /><br />Periodo-clausola, non esegue il mapping alla semantica di SQL Server|  
|DELETE-istruzione|**Mappe SSMA eliminare con le eccezioni seguenti:**<br /><br />Riferimento alla tabella clausola - Only-tabella-riferimenti non è mappata a una semantica SQL server<br /><br />Clausola periodo: non esegue il mapping alla semantica di SQL Server|  
|Livello di isolamento e il tipo di blocco|Viene eseguito il mapping.|  
|Procedure (SQL)|Viene eseguito il mapping.|  
|Procedure (esterno)|Richiedono l'aggiornamento manuale.|  
|Procedure (originate)|Non sono mappati a una semantica di SQL Server.|  
|Istruzione di assegnazione|Viene eseguito il mapping.|  
|Istruzione CALL per una procedura|Viene eseguito il mapping.|  
|Istruzione CASE|Viene eseguito il mapping.|  
|Istruzione FOR|Viene eseguito il mapping.|  
|GOTO - istruzione|Viene eseguito il mapping.|  
|Istruzione IF|Viene eseguito il mapping.|  
|L'istruzione di ITERAZIONE|Viene eseguito il mapping.|  
|LASCIARE l'istruzione|Viene eseguito il mapping.|  
|Istruzione di ciclo|Viene eseguito il mapping.|  
|Ripetere l'istruzione|Viene eseguito il mapping.|  
|RESIGNAL istruzione|Le condizioni non sono supportate. I messaggi possono essere facoltativi.|  
|Istruzione RETURN|Viene eseguito il mapping.|  
|Istruzione di segnale|Le condizioni non sono supportate. I messaggi possono essere facoltativi.|  
|WHILE (istruzione)|Viene eseguito il mapping.|  
|GET (istruzione) diagnostica|**SSMA viene eseguito il mapping ottenere diagnostica con le eccezioni seguenti:**<br /><br />Viene eseguito il mapping ROW_COUNT.<br /><br />Viene eseguito il mapping DB2_RETURN_STATUS.<br /><br />Viene eseguito il mapping Testo_Messaggio.<br /><br />DB2_SQL_NESTING_LEVEL - non esegue il mapping alla semantica di SQL Server<br /><br />DB2_TOKEN_STRING - non esegue il mapping alla semantica di SQL Server|  
|Cursori|**SSMA viene eseguito il mapping dei CURSORI con le eccezioni seguenti:**<br /><br />Istruzione di cursore ALLOCATE - non esegue il mapping alla semantica di SQL Server<br /><br />Istruzione di ASSOCIARE i LOCALIZZATORI - non esegue il mapping alla semantica di SQL Server<br /><br />Istruzione DECLARE CURSOR - clausola Returnability non è mappata a una semantica SQL server<br /><br />L'istruzione FETCH - mapping parziale. Sono supportate solo le variabili come destinazione. DESCRITTORE SQLDA non è mappata a una semantica SQL server|  
|Variabili|Viene eseguito il mapping.|  
|Le eccezioni, i gestori e condizioni|**SSMA esegue il mapping di "eccezioni" con le eccezioni seguenti:**<br /><br />Esci gestori: viene eseguito il mapping.<br /><br />ANNULLARE i gestori: viene eseguito il mapping.<br /><br />CONTINUARE i gestori: non sono mappati.<br /><br />Condizioni - non esegue il mapping alla semantica SQL server.|  
|SQL dinamica|Non è mappata.|  
|Alias|Viene eseguito il mapping.|  
|Nomi alternativi|Mapping parziale. È necessaria per l'oggetto sottostante l'elaborazione manuale|  
|Sinonimi|Viene eseguito il mapping.|  
|Funzioni standard in DB2|SSMA esegue il mapping di funzioni standard di DB2 quando una funzione equivalente è disponibile in SQL Server:|  
|Autorizzazione|Non è mappata.|  
|Predicati|Viene eseguito il mapping.|  
|SELECT INTO - istruzione|Non è mappata.|  
|I valori nell'istruzione|Non è mappata.|  
|Controllo delle transazioni|Non è mappata.|  
  
## <a name="converting-db2-database-objects"></a>Conversione di oggetti di Database DB2  
Per convertire gli oggetti di database di DB2, prima di tutto selezionare gli oggetti che si desidera convertire e quindi SSMA eseguire la conversione. Per visualizzare i messaggi di output durante la conversione nel **View** dal menu **Output**.  
  
**Per convertire gli oggetti di DB2 in sintassi SQL Server**  
  
1.  Nel Visualizzatore metadati DB2, espandere il server DB2 e infine **schemi**.  
  
2.  Selezionare gli oggetti da convertire:  
  
    -   Per convertire tutti gli schemi, selezionare la casella di controllo accanto a **schemi**.  
  
    -   Per convertire o omettere un database, selezionare la casella di controllo accanto al nome dello schema.  
  
    -   Per convertire o omettere una categoria di oggetti, espandere uno schema, quindi selezionare o deselezionare la casella di controllo accanto alla categoria.  
  
    -   Per convertire o omettere singoli oggetti, espandere la cartella di categoria, quindi selezionare o deselezionare la casella di controllo accanto all'oggetto.  
  
3.  Per convertire tutti gli oggetti selezionati, fare doppio clic su **schemi** e selezionare **Converti Schema**.  
  
    È anche possibile convertire gli oggetti singoli o categorie di oggetti pulsante destro del mouse relativa cartella padre o l'oggetto e quindi selezionando **convertire lo Schema**.  
  
## <a name="viewing-conversion-problems"></a>Visualizzazione dei problemi di conversione  
Alcuni oggetti DB2 potrebbero non essere convertiti. È possibile determinare i tassi di conversione riuscita, visualizzando il report di riepilogo di conversione.  
  
**Per visualizzare un report di riepilogo**  
  
1.  Nel Visualizzatore metadati DB2, selezionare **schemi**.  
  
2.  Nel riquadro di destra, selezionare la **Report** scheda.  
  
    Questo report mostra il report di riepilogo di valutazione per tutti gli oggetti di database che sono state valutate o convertiti. È anche possibile visualizzare un report di riepilogo per i singoli oggetti:  
  
    -   Per visualizzare il report per un singolo schema, selezionare lo schema in Esplora i metadati di DB2.  
  
    -   Per visualizzare il report per un singolo oggetto, selezionare l'oggetto in Visualizzatore metadati DB2. Gli oggetti che presentano problemi di conversione hanno un'icona rossa di errore.  
  
Per gli oggetti che non hanno superato la conversione, è possibile visualizzare la sintassi che ha generato l'errore di conversione.  
  
**Per visualizzare i problemi di conversione singoli**  
  
1.  Nel Visualizzatore metadati DB2, espandere **schemi**.  
  
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
  
-   È possibile modificare l'oggetto nel database di DB2 per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [ci si connette al Database DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
-   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati ed Esplora i metadati di DB2, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la migrazione dei dati da DB2.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [caricare gli oggetti convertiti in SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione di dati DB2 in SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
