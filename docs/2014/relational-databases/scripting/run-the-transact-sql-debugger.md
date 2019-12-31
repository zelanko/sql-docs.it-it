---
title: Esecuzione del debugger Transact-SQL
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, sysadmin requirement
- Transact-SQL debugger, supported versions
- Query Editor [Database Engine], right-click menu
- Transact-SQL debugger, Query Editor shortcut menu
- Transact-SQL debugger, stopping
- Transact-SQL debugger, Debug menu
- Transact-SQL debugger, Debug toolbar
- Transact-SQL debugger, keyboard shortcuts
- Transact-SQL debugger, starting
ms.assetid: 386f6d09-dbec-4dc7-9e8a-cd9a4a50168c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 843bd1c4213b6cb50c843b846cd9f5d95529b4b1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243698"
---
# <a name="run-the-transact-sql-debugger"></a>Esecuzione del debugger Transact-SQL
  È possibile avviare il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] dopo avere aperto una finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . È quindi possibile eseguire il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] in modalità di debug fino a quando non si desidera arrestare il debugger. È possibile impostare le opzioni desiderate per personalizzare la modalità di esecuzione del debugger.  
  
## <a name="starting-and-stopping-the-debugger"></a>Avvio e arresto del debugger  
 Di seguito vengono indicati i requisiti per avviare il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
-   Se l'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] è connesso a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in un altro computer, è necessario aver configurato il debugger per il debug remoto. Per ulteriori informazioni, vedere [la pagina relativa alla configurazione del debugger Transact-SQL](configure-firewall-rules-before-running-the-tsql-debugger.md).  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] deve essere eseguito con un account di Windows membro del ruolo predefinito del server sysadmin.  
  
-   La finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve essere connessa tramite un account di accesso con autenticazione di Windows o con autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che sia membro del ruolo predefinito del server sysadmin.  
  
-   La finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve essere connessa a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 (SP2) o versione successiva. Non è possibile eseguire il debugger quando la finestra dell'editor di query è connessa a un'istanza che è in modalità utente singolo.  
  
 Si consiglia di eseguire il debug del codice [!INCLUDE[tsql](../../includes/tsql-md.md)] su un server di prova, anziché un server di produzione, per le ragioni che seguono:  
  
-   Il debug è un'operazione che richiede privilegi elevati. Solo i membri del ruolo predefinito del server sysadmin possono pertanto eseguire il debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Le sessioni di debug spesso durano a lungo perché comportano il controllo dell'esecuzione di numerose istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] . I blocchi, ad esempio i blocchi di aggiornamento, che vengono acquisiti dalla sessione potrebbero essere mantenuti per lunghi periodi di tempo, fino al termine della sessione o al commit o rollback della transazione.  
  
 All'avvio del debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] , la finestra dell'editor di query entra nella modalità di debug e l'esecuzione del codice viene sospesa dal debugger in corrispondenza della prima riga. A questo punto, è possibile procedere istruzione per istruzione, sospendere l'esecuzione su istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] specifiche e utilizzare le finestre del debugger per visualizzare lo stato corrente dell'esecuzione: È possibile avviare il debugger facendo clic sul pulsante **Debug** nella barra degli strumenti **Query** oppure scegliendo **Avvia debug** dal menu **Debug** .  
  
 La finestra dell'editor di query rimane in modalità di debug sino al termine dell'ultima istruzione nella finestra dell'editor di query oppure fino a quando non viene arrestata la modalità di debug. È possibile arrestare l'esecuzione della modalità di debug e di un'istruzione utilizzando uno dei metodi seguenti:  
  
-   Scegliere **Arresta debug** dal menu **Debug**.  
  
-   Nella barra degli strumenti **Debug** fare clic sul pulsante **Arresta debug** .  
  
-   Scegliere **Annulla esecuzione query** dal menu **Query**.  
  
-   Nella barra degli strumenti **Query** fare clic sul pulsante **Annulla esecuzione query** .  
  
 È inoltre possibile arrestare la modalità di debug e consentire il completamento delle restanti istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] scegliendo **Disconnetti tutto** dal menu **Debug** .  
  
## <a name="controlling-the-debugger"></a>Controllo del debugger  
 È possibile controllare l'esecuzione del debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando i comandi, le barre degli strumenti e le scelte rapide seguenti:  
  
-   Il menu **Debug** e la barra degli strumenti **Debug** . Sia il menu **Debug** che la barra degli strumenti **Debug** sono inattivi fino a quando non viene attivata una finestra dell'editor di query aperta. Rimangono attivi fino alla chiusura del progetto corrente.  
  
-   Le scelte rapide da tastiera per il debugger.  
  
-   Il menu di scelta rapida dell'editor di query. Il menu di scelta rapida viene visualizzato quando si fa clic con il pulsante destro del mouse su una riga in una finestra dell'editor di query. Quando la finestra dell'editor di query è in modalità di debug, nel menu di scelta rapida vengono visualizzati i comandi del debugger applicabili alla riga o stringa selezionata.  
  
-   Le voci di menu e i comandi contestuali nelle finestre aperte dal debugger, ad esempio le finestre **Espressione di controllo** o la finestra **Punti di interruzione** .  
  
 Nella tabella seguente sono illustrati i comandi di menu del debugger, i pulsanti della barra degli strumenti e i tasti di scelta rapida.  
  
|Comando del menu Debug|Comando di scelta rapida dell'editor|Pulsante della barra degli strumenti|Tasto di scelta rapida|Azione|  
|------------------------|-----------------------------|--------------------|-----------------------|------------|  
|**Windows/punti di interruzione**|Non disponibile|**Interruzione**|CTRL+ALT+B|Consente di visualizzare la finestra **Punti di interruzione** nella quale è possibile visualizzare e gestire i punti di interruzione.|  
|**Windows/Watch/Controllo1**|Non disponibile|**Punti di interruzione/espressione di controllo/Controllo1**|CTRL+ALT+W, 1|Consente di visualizzare la finestra **Espressione di controllo1** .|  
|**Windows/Watch/Controllo2**|Non disponibile|**Punti di interruzione/espressione di controllo/Controllo2**|CTRL+ALT+W, 2|Consente di visualizzare la finestra **Espressione di controllo2** .|  
|**Windows/Watch/Controllo3**|Non disponibile|**Punti di interruzione/espressione di controllo/Controllo3**|CTRL+ALT+W, 3|Visualizzare la finestra **Espressione di controllo3** .|  
|**Windows/Watch/Controllo4**|Non disponibile|**Punti di interruzione/espressione di controllo/Controllo4**|CTRL+ALT+W, 4|Consente di visualizzare la finestra **Espressione di controllo4** .|  
|**Windows/variabili locali**|Non disponibile|**Punti di interruzione/variabili locali**|CTRL+ALT+V, L|Visualizzare la finestra **variabili locali** .|  
|**Windows/stack di chiamate**|Non disponibile|**Punti di interruzione/stack di chiamate**|CTRL+ALT+C|Visualizzare la finestra **stack di chiamate** .|  
|**Windows/thread**|Non disponibile|**Punti di interruzione/thread**|CTRL+ALT+H|Visualizzare la finestra **thread** .|  
|**Continuare**|Non disponibile|**Continuare**|ALT+F5|Eseguire il codice fino al successivo punto di interruzione. **Continua** non è attivo fino a quando non viene attivata una finestra dell'editor di query in modalità di debug.|  
|**Avvia debug**|Non disponibile|**Avvia debug**|ALT+F5|Consente di attivare la modalità di debug per una finestra dell'editor di query ed eseguire il codice fino al primo punto di interruzione. Se lo stato attivo si trova in una finestra dell'editor di query in modalità di debug, **Avvia debug** viene sostituito da **Continua**.|  
|**Interrompi tutto**|Non disponibile|**Interrompi tutto**|CTRL+ALT+INTERR|Questa caratteristica non è utilizzata dal debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**Arresta debug**|Non disponibile|**Arresta debug**|MAIUSC+F5|Consente di portare una finestra dell'editor di query dalla modalità di debug alla modalità normale.|  
|**Scollega tutto**|Non disponibile|Non disponibile|Non disponibile|Consente di arrestare la modalità di debug, ma di eseguire le istruzioni restanti nella finestra dell'editor di query.|  
|**Esegui istruzione**|Non disponibile|**Esegui istruzione**|F11|Consente di eseguire l'istruzione successiva e anche di aprire una nuova finestra dell'editor di query nella modalità di debug se l'istruzione successiva esegue una stored procedure, un trigger o una funzione.|  
|**Esegui istruzione/routine**|Non disponibile|**Esegui istruzione/routine**|F10|Stessa funzione di **Esegui istruzione**eccetto per il fatto che con questo comando non viene eseguito il debug di funzioni, stored procedure o trigger.|  
|**Esci da istruzione/uscita**|Non disponibile|**Esci da istruzione/uscita**|MAIUSC+F11|Consente di eseguire il codice restante in un trigger, una funzione o una stored procedure ignorando i punti di interruzione. La normale modalità di debug riprende quando il controllo viene restituito al codice che ha chiamato il modulo.|  
|Non disponibile|**Esegui fino a** Cursore|Non disponibile|CTRL+F10|Consente di eseguire tutto il codice dall'ultima posizione di arresto fino alla posizione corrente del cursore ignorando i punti di arresto.|  
|**Controllo immediato**|**Controllo immediato**|Non disponibile|CTRL+ALT+Q|Consente di visualizzare la finestra **Controllo immediato** .|  
|**Imposta/Rimuovi punto di interruzione**|**Punto di interruzione/Inserisci punto di interruzione**|Non disponibile|F9|Consente di inserire un punto di interruzione in corrispondenza dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrente o selezionata.|  
|Non disponibile|**Punto di interruzione/Elimina punto di interruzione**|Non disponibile|Non disponibile|Consente di eliminare il punto di interruzione dalla riga selezionata.|  
|Non disponibile|**Punto di interruzione/Disabilita punto di interruzione**|Non disponibile|Non disponibile|Consente di disabilitare il punto di interruzione nella riga selezionata. Il punto di interruzione rimane sulla riga di codice, ma l'esecuzione non verrà arrestata fino a quando non sarà riattivata.|  
|Non disponibile|**Punto di interruzione/Abilita punto di interruzione**|Non disponibile|Non disponibile|Consente di attivare il punto di interruzione nella riga selezionata.|  
|**Elimina tutti i punti di interruzione**|Non disponibile|Non disponibile|CTRL+MAIUSC+F9|Consente di eliminare tutti i punti di interruzione.|  
|**Disabilitare tutti i punti di interruzione**|Non disponibile|Non disponibile|Non disponibile|Consente di disabilitare tutti i punti di interruzione.|  
|Non disponibile|**Aggiungi espressione di controllo**|Non disponibile|Non disponibile|Consente di aggiungere l'espressione selezionata alla finestra **Espressione di controllo** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](transact-sql-debugger.md)   
 [Eseguire il codice Transact-SQL](step-through-transact-sql-code.md)   
 [Informazioni del debugger Transact-SQL](transact-sql-debugger-information.md)   
 [Editor di query motore di database &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)  
  
  
