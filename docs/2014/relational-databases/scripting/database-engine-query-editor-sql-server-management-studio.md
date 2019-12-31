---
title: editor di query del Motore di database
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ec7e26daa91723e5633a9640b99003ebc844d31
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244938"
---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>Editor di query del Motore di database (SQL Server Management Studio)
  Utilizzare l'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per creare ed eseguire script contenenti istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] . L'editor supporta anche l'esecuzione di script contenenti comandi **sqlcmd** .  
  
## <a name="transact-sql-f1-help"></a>Guida di Transact-SQL  
 L'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] supporta il collegamento all'argomento di riferimento per un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] specifica quando si seleziona F1. A tale scopo, evidenziare il nome di un'istruzione Transact-SQL, quindi selezionare F1. Verrà cercato quindi un argomento che disponga di un attributo della Guida corrispondente alla stringa evidenziata.  
  
 Se non vengono trovati argomenti con una parola chiave della Guida che corrisponde esattamente alla stringa evidenziata, verrà visualizzato questo argomento. In tal caso, esistono due approcci per trovare le informazioni che si stanno cercando:  
  
-   Copiare e incollare la stringa dell'editor evidenziata nella scheda di ricerca della documentazione online di SQL Server o effettuare una ricerca.  
  
-   Evidenziare solo la parte dell'istruzione Transact-SQL con maggiori probabilità di corrispondenza a una parola chiave della Guida applicata a un argomento e selezionare di nuovo F1. Il motore di ricerca richiede una corrispondenza esatta tra la stringa evidenziata e una parola chiave della Guida assegnata a un argomento. Se la stringa evidenziata contiene elementi univoci dell'ambiente, ad esempio nomi di colonna o di parametro, il motore di ricerca non restituirà corrispondenze. Di seguito sono riportati alcuni esempi di stringhe evidenziabili:  
  
    -   Nome dell'istruzione Transact-SQL, ad esempio SELECT, CREATE DATABASE o BEGIN TRANSACTION.  
  
    -   Nome di una funzione predefinita, ad esempio SERVERPROPERTY o @@VERSION.  
  
    -   Nome di una tabella di stored procedure di sistema o di una vista, ad esempio sys.data_spaces o sp_tableoption.  
  
## <a name="working-with-the-database-engine-query-editor"></a>Utilizzo dell'editor di query del Motore di database  
 L'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] è uno dei quattro editor implementati in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per una descrizione della funzionalità implementata nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e delle attività principali che è possibile eseguire tramite l'editor, vedere [Editor di query e di testo &#40;SQL Server Management Studio&#41;](../scripting/query-and-text-editors-sql-server-management-studio.md).  
  
## <a name="sql-editor-toolbar"></a>Barra degli strumenti Editor SQL  
 Quando l'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] è aperto, nella barra degli strumenti Editor SQL sono visualizzati i pulsanti seguenti.  
  
 **Connettersi**  
 Consente di aprire la finestra di dialogo **Connetti al server** . Utilizzare questa finestra di dialogo per stabilire una connessione a un server.  
  
 **Disconnettere**  
 Disconnette l'editor di query corrente dal server.  
  
 **Cambia connessione**  
 Consente di aprire la finestra di dialogo **Connetti al server** . Utilizzare questa finestra di dialogo per stabilire una connessione a un server diverso.  
  
 **Nuova query con connessione corrente**  
 Consente di aprire una nuova finestra dell'editor di query e di utilizzare le stesse informazioni di connessione della finestra dell'editor di query corrente.  
  
 **Database disponibili**  
 Consente di passare a un database diverso sullo stesso server.  
  
 **Eseguire**  
 Consente di eseguire il codice selezionato o, se non è selezionata alcuna parte del codice, di eseguire tutto il codice incluso nell'editor di query.  
  
 **Debug**  
 Consente di abilitare il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] , che supporta azioni di debug quali l'impostazione di punti di interruzione, il controllo di variabili e l'esecuzione di codice istruzione per istruzione.  
  
 **Annulla esecuzione query**  
 Consente di inviare una richiesta di annullamento al server. Alcune query non possono essere annullate immediatamente, ma devono attendere una condizione di annullamento adatta. Quando le transazioni vengono annullate, è possibile che si verifichino ritardi durante il rollback delle transazioni.  
  
 **Analizzare**  
 Consente di controllare la sintassi del codice selezionato. Se non è selezionata alcuna parte del codice, viene controllata la sintassi di tutto il codice incluso nella finestra dell'editor di query.  
  
 **Visualizza piano di esecuzione stimato**  
 Richiede un piano di esecuzione query a Query Processor senza eseguire effettivamente la query e visualizza il piano nella finestra **Piano di esecuzione** . In tale piano vengono utilizzate statistiche dell'indice per stimare il numero di righe restituite previste durante ogni parte dell'esecuzione della query. Il piano di query effettivo utilizzato può differire dal piano di esecuzione stimato. Ciò si verifica in presenza di una differenza significativa tra il numero di righe restituite e quelle stimate. In questo caso, Query Processor modifica il piano per renderlo più efficiente.  
  
 **Opzioni query**  
 Consente di aprire la finestra di dialogo **Opzioni query** . Utilizzare questa finestra di dialogo per configurare le opzioni predefinite per l'esecuzione della query e per i relativi risultati.  
  
 **IntelliSense abilitato**  
 Consente di specificare se la funzionalità IntelliSense è disponibile o meno nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 **Includi piano di esecuzione effettivo**  
 Consente di eseguire la query e di restituirne i risultati insieme al piano di esecuzione utilizzato per la query. Questi elementi vengono visualizzati come piano di query grafico nella finestra **Piano di esecuzione** .  
  
 **Includi statistiche client**  
 Include una finestra **Statistiche client** contenente statistiche relative alla query e ai pacchetti di rete, nonché al tempo trascorso dall'inizio della query.  
  
 **Risultati in formato testo**  
 Restituisce i risultati della query in formato testo nella finestra **Risultati** .  
  
 **Risultati in formato griglia**  
 Restituisce i risultati della query sotto forma di una o più griglie nella finestra **Risultati** .  
  
 **Risultati in un file**  
 All'esecuzione della query viene visualizzata la finestra di dialogo **Salva risultati** . In **Salva in**selezionare la cartella in cui si desidera salvare il file. In **Nome file**digitare il nome del file e quindi fare clic su **Salva** per salvare i risultati della query come file **Report** con estensione rpt. Per visualizzare le opzioni avanzate, fare clic sulla freccia rivolta verso il basso del pulsante **Salva** e quindi selezionare **Salva con codifica**.  
  
 **Selezione Commenti**  
 Consente di contrassegnare la riga corrente come commento tramite l'aggiunta di un operatore di commento (--) all'inizio della riga.  
  
 **Rimuovi commento selezione**  
 Consente di modificare la riga corrente in istruzione di origine attiva rimuovendo eventuali operatori di commento (--) presenti all'inizio della riga.  
  
 **Riduci rientro riga**  
 Consente di spostare a sinistra il testo della riga rimuovendo spazi vuoti all'inizio della riga.  
  
 **Aumenta rientro riga**  
 Consente di spostare a destra il testo della riga aggiungendo spazi vuoti all'inizio della riga.  
  
 **Specificare i valori per i parametri del modello**  
 Consente di aprire una finestra di dialogo in cui è possibile specificare valori per i parametri inclusi in stored procedure e funzioni.  
  
 È anche possibile aggiungere la barra degli strumenti Editor SQL selezionando il menu **Visualizza** , **Barre degli strumenti**, quindi **Editor SQL**. Se la barra degli strumenti Editor SQL viene aggiunta quando non sono aperte finestre dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , non è disponibile alcun pulsante.  
  
## <a name="sql-editor-toolbar"></a>Barra degli strumenti Editor SQL  
 Quando è aperta una finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , è possibile aggiungere la barra degli strumenti Debug scegliendo **Barre degli strumenti** dal menu **Visualizza**e quindi facendo clic su **Debug**. Se la barra degli strumenti Debug viene aggiunta quando non è aperta alcuna finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , non sarà disponibile alcun pulsante.  
  
 **Continuare**  
 Consente di eseguire il codice nella finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] fino a quando non viene rilevato un punto di interruzione.  
  
 **Interrompi tutto**  
 Consente di impostare il debugger per l'interruzione di tutti i processi a cui è connesso il debugger stesso quando si verifica un'interruzione.  
  
 **Arresta debug**  
 Consente di disattivare la modalità di debug per la finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e di ripristinare la modalità di esecuzione predefinita.  
  
 **Mostra istruzione successiva**  
 Consente di spostare il cursore in corrispondenza dell'istruzione successiva da eseguire.  
  
 **Esegui istruzione**  
 Viene eseguita l'istruzione successiva. Se l'istruzione chiama una stored procedure, una funzione o un trigger Transact-SQL, il debugger visualizza una nuova finestra dell' **editor di query** contenente il codice del modulo. La finestra sarà in modalità di debug e l'esecuzione verrà sospesa in corrispondenza della prima istruzione nel modulo. È quindi possibile spostarsi nel modulo, ad esempio, impostando punti di interruzione o avanzando istruzione per istruzione nel codice.  
  
 **Esegui istruzione/routine**  
 Viene eseguita l'istruzione successiva. Se l'istruzione richiama una stored procedure, una funzione o un trigger Transact-SQL, il modulo viene eseguito fino alla fine e i risultati vengono restituiti al codice che ha effettuato la chiamata. Se si è certi che non vi siano errori nel modulo, è possibile continuare. L'esecuzione viene sospesa in corrispondenza dell'istruzione che segue la chiamata al modulo.  
  
 **Esci da istruzione/uscita**  
 Consente di tornare al successivo livello di chiamata più alto, ad esempio una funzione, una stored procedure o un trigger. L'esecuzione viene sospesa in corrispondenza dell'istruzione che segue la chiamata alla stored procedure, la funzione o il trigger.  
  
 **Windows**  
 Consente di aprire la finestra **Punto di interruzione** o **Controllo immediato** .  
  
## <a name="see-also"></a>Vedere anche  
 [Tasti di scelta rapida SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
