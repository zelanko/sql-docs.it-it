---
description: Gestione guidata partizione
title: Gestione guidata partizione
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
f1_keywords:
- sql13.swb.managepartition.createjob.f1
- sql13.swb.managepartition.progress.f1
- sql13.swb.managepartition.getstart.f1
- sql13.swb.managepartition.selectswitchtables.f1
- sql13.swb.managepartition.stagingtable.f1
- sql13.swb.managepartition.switchin.f1
- sql13.swb.managepartition.switchout.f1
- sql13.swb.managepartition.partitionaction.f1
- sql13.swb.managepartition.summary.f1
- sql13.swb.managepartition.selectoutput.f1
helpviewer_keywords:
- wizards [SQL Server Management Studio] See Manage Partition Wizard
ms.assetid: e2478d26-dea4-428d-98c5-aad2d2a30da8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 45cfba1078dbe72e09f760f24fc0c9f47c0c0b1f
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891021"
---
# <a name="manage-partition-wizard"></a>Gestione guidata partizione 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Usare la **Gestione guidata partizione** per gestire e modificare tabelle partizionate esistenti tramite il cambio della partizione o l'implementazione di uno scenario basato su finestra temporale scorrevole. Questa procedura guidata può semplificare la gestione delle partizioni e la normale migrazione di dati all'interno e all'esterno delle tabelle.  
  
### <a name="to-start-the-manage-partition-wizard"></a>Per avviare la Gestione guidata partizione  
  
-   In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]selezionare il database, fare clic con il pulsante destro del mouse sulla tabella in cui si desidera creare partizioni, scegliere **Archiviazione**e quindi fare clic su **Gestione partizione**.  
  
     **Nota** Se **Gestione partizione** non è disponibile, potrebbe essere stata selezionata una tabella che non contiene partizioni. Fare clic su **Crea partizione** nel sottomenu **Archiviazione** e usare la **Creazione guidata partizione** per creare partizioni nella tabella.  
  
 Per informazioni generali su indici e partizioni, vedere [Tabelle e indici partizionati](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Questa sezione include le informazioni necessarie per gestire, modificare e implementare partizioni tramite la **Gestione guidata partizione**.  
  
##  <a name="in-this-section"></a><a name="Top"></a> Contenuto della sezione  
 Le sezioni seguenti forniscono informazioni sulle pagine della **Gestione guidata partizione**.  
  
 [Gestione guidata partizione (pagina Selezionare un'azione relativa alla partizione)](#SelectPartitionAction)  
  
 [Gestione guidata partizione (pagina Attiva)](#SwitchIn)  
  
 [Gestione guidata partizione (pagina Disattiva)](#SwitchOut)  
  
 [Gestione guidata partizione (pagina Seleziona opzioni per la tabella di gestione temporanea)](#StagingTableOptions)  
  
 [Gestione guidata partizione (pagina Seleziona un'opzione di output)](#OutputOption)  
  
 [Gestione guidata partizione (pagina Nuova pianificazione processo)](#NewJob)  
  
 [Gestione guidata partizione (pagina Riepilogo)](#Summary)  
  
 [Gestione guidata partizione (pagina Stato)](#Progress)  
  
##  <a name="select-partition-action-page"></a><a name="SelectPartitionAction"></a> Pagina Selezionare un'azione relativa alla partizione  
 Usare la pagina **Selezionare un'azione relativa alla partizione** per scegliere l'azione che si desidera eseguire sulla partizione.  
  
### <a name="create-a-staging-table"></a>Creazione di una tabella di gestione temporanea  
 Il cambio della partizione rappresenta un'attività di partizionamento comune se si dispone di una tabella partizionata in e da cui si esegue regolarmente la migrazione di dati, ad esempio se si dispone di una tabella partizionata in cui vengono archiviati dati trimestrali correnti ed è necessario spostare nuovi dati e archiviare i dati precedenti al termine di ogni trimestre.  
  
 La procedura guidata consente di progettare la tabella di staging con la stessa colonna di partizionamento, la stessa struttura di tabelle e colonne e gli stessi indici e di archiviare la nuova tabella nel filegroup in cui è inclusa la partizione di origine.  
  
 Per creare una tabella di staging in cui e da cui spostare i dati della partizione, selezionare **Crea tabella di staging per il cambio della partizione**.  
  
### <a name="sliding-window-scenario"></a>Scenario basato su finestra temporale scorrevole  
 Per gestire le partizioni in uno scenario basato su finestra temporale scorrevole, selezionare **Gestisci dati partizionati in uno scenario basato su finestra temporale scorrevole**.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
 **Crea tabella di staging per il cambio della partizione**  
 Consente di creare una tabella di staging per i dati da spostare all'interno o all'esterno della tabella partizionata esistente.  
  
 **Partizione di disattivazione**  
 Fornisce le opzioni per la rimozione di una partizione dalla tabella.  
  
 **Partizione di attivazione**  
 Fornisce le opzioni per l'aggiunta di una partizione alla tabella.  
  
 **Gestisci dati partizionati in uno scenario basato su finestra temporale scorrevole**  
 Consente di aggiungere una partizione vuota alla tabella esistente da utilizzare per spostare i dati. La procedura guidata supporta attualmente lo spostamento all'interno dell'ultima partizione e all'esterno della prima partizione.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="select-partition-switching-in-options-page"></a><a name="SwitchIn"></a> Pagina Seleziona opzioni per l'attivazione della partizione  
 Usare la pagina **Seleziona opzioni per l'attivazione della partizione** per selezionare la tabella di staging che si desidera attivare nella tabella partizionata.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
 **Mostra tutte le partizioni**  
 Selezionare questa opzione per visualizzare tutte le partizioni, incluse le partizioni correnti nella tabella partizionata.  
  
 **Griglia partizione**  
 Consente di visualizzare il nome della partizione e i valori per **Limite sinistro**, **Limite destro**, **Filegroup**e **Conteggio righe** delle partizioni selezionate.  
  
 **Tabella di attivazione**  
 Consente di selezionare la tabella di staging contenente la partizione che si desidera aggiungere alla tabella partizionata. È necessario creare questa tabella di staging prima di attivare partizioni usando la **Gestione guidata partizione**.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="select-partition-switching-out-options-page"></a><a name="SwitchOut"></a> Pagina Seleziona opzioni per la disattivazione della partizione  
 Usare la pagina **Seleziona opzioni per la disattivazione della partizione** per selezionare la partizione e la tabella di staging contenente i dati partizionati che si desidera disattivare dalla tabella partizionata.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
 **Griglia partizione**  
 Consente di visualizzare il nome della partizione e i valori per **Limite sinistro**, **Limite destro**, **Filegroup**e **Conteggio righe** delle partizioni selezionate.  
  
 **Tabella di disattivazione**  
 Consente di scegliere una nuova tabella o una esistente in cui spostare i dati.  
  
 **Nuovo**  
 Consente di immettere un nuovo nome per la tabella di staging che si desidera utilizzare per la partizione da disattivare per la tabella di origine corrente.  
  
 **Esistente**  
 Consente di selezionare una tabella di staging esistente che si desidera utilizzare per la partizione che si desidera disattivare per la tabella di origine corrente. Gli eventuali dati contenuti nella tabella verranno sovrascritti con i dati utilizzati per la disattivazione.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="select-the-staging-table-options-page"></a><a name="StagingTableOptions"></a> Pagina Seleziona opzioni per la tabella di gestione temporanea  
 Usare la pagina **Seleziona opzioni per la tabella di staging** per creare la tabella di staging che si desidera utilizzare per lo spostamento dei dati partizionati.  
  
 Le tabelle di gestione temporanea devono risiedere nello stesso filegroup della partizione selezionata in cui è presente la tabella di origine. La tabella di staging deve riflettere la struttura della tabella di origine e della tabella di destinazione.  
  
 È inoltre possibile creare gli stessi indici nella tabella di staging presenti nella partizione di origine. La tabella di staging contiene automaticamente un vincolo basato sugli elementi della partizione di origine. In genere tale vincolo viene generato dal valore limite della partizione di origine.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
 **Nome tabella di gestione temporanea**  
 Consente di creare un nome per la tabella di staging o di accettare il nome predefinito visualizzato nella casella di modifica.  
  
 **Cambia partizione**  
 Consente di selezionare la partizione di origine che si desidera rimuovere dalla tabella corrente.  
  
 **Nuovo valore limite**  
 Consente di selezionare o di immettere il valore limite desiderato per la partizione nella tabella di staging.  
  
 **Filegroup**  
 Consente di selezionare un filegroup per la nuova tabella.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="select-output-option-page"></a><a name="OutputOption"></a> Pagina Seleziona un'opzione di output  
 Usare la pagina **Seleziona un'opzione di output** per specificare il modo in cui si desidera completare le modifiche alle partizioni.  
  
### <a name="create-script"></a>Crea script  
 Al termine della procedura guidata, nell'editor di query viene creato uno script per la modifica delle partizioni nella tabella. Selezionare **Crea script** se si desidera controllare lo script e quindi eseguirlo manualmente.  
  
 **Genera script nel file**  
 Consente di generare lo script in un file con estensione sql. Specificare **Unicode** o **Testo ANSI**. Per specificare un nome e un percorso per il file, scegliere **Sfoglia**.  
  
 **Genera script negli Appunti**  
 Consente di salvare lo script negli Appunti.  
  
 **Genera script in nuova finestra Query**  
 Consente di generare lo script in una finestra dell'editor di query. Se non è aperta alcuna finestra dell'editor, ne viene aperta una nuova da utilizzare come destinazione per lo script.  
  
### <a name="run-immediately"></a>Esegui immediatamente  
 **Run immediately**  
 Per completare l'applicazione di modifiche alle partizioni nella procedura guidata, fare clic su **Avanti** o **Fine**.  
  
### <a name="schedule"></a>Pianificazione  
 Selezionare questa opzione per modificare le partizioni della tabella a una data e a un'ora pianificata.  
  
 **Cambia pianificazione**  
 Viene aperta la finestra di dialogo **Nuova pianificazione processo** , in cui è possibile selezionare, modificare o visualizzare le proprietà del processo pianificato.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="new-job-schedule-page"></a><a name="NewJob"></a> Pagina Nuova pianificazione processo  
 Usare la pagina **Nuova pianificazione processo** per visualizzare e modificare le proprietà della pianificazione.  
  
### <a name="options"></a>Opzioni  
 Selezionare il tipo di pianificazione desiderata per il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Nome**  
 Consente di digitare un nuovo nome per la pianificazione.  
  
 **Processi nella pianificazione**  
 Consente di visualizzare i processi esistenti che utilizzano la pianificazione.  
  
 **Tipo pianificazione**  
 Consente di selezionare il tipo di pianificazione.  
  
 **Enabled**  
 Consente di abilitare o disabilitare la pianificazione.  
  
### <a name="recurring-schedule-types-options"></a>Opzioni relative ai tipi di pianificazione periodica  
 Selezionare la frequenza del processo pianificato.  
  
 **Ricorrenza**  
 Consente di selezionare l'intervallo in base al quale ripetere la pianificazione.  
  
 **Ogni**  
 Consente di selezionare il numero di giorni o di settimane quale intervallo di esecuzione delle pianificazioni. Questa opzione non è disponibile per pianificazioni mensili.  
  
 **Lunedì**  
 Consente di impostare l'esecuzione del processo ogni lunedì. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Martedì**  
 Consente di impostare l'esecuzione del processo ogni martedì. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Mercoledì**  
 Consente di impostare l'esecuzione del processo ogni mercoledì. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Giovedì**  
 Consente di impostare l'esecuzione del processo ogni giovedì. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Venerdì**  
 Consente di impostare l'esecuzione del processo ogni venerdì. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Sabato**  
 Consente di impostare l'esecuzione del processo ogni sabato. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Domenica**  
 Consente di impostare l'esecuzione del processo ogni domenica. Questa opzione è disponibile solo per pianificazioni settimanali.  
  
 **Day**  
 Consente di selezionare il giorno del mese in cui eseguire la pianificazione. Questa opzione è disponibile solo per pianificazioni mensili.  
  
 **ogni**  
 Consente di selezionare il numero di mesi tra una pianificazione e l'altra. Questa opzione è disponibile solo per pianificazioni mensili.  
  
 **Ogni**  
 Consente di specificare una pianificazione per un giorno specifico di una determinata settimana del mese. Questa opzione è disponibile solo per pianificazioni mensili.  
  
 **Una sola volta alle**  
 Consente di impostare l'ora per l'esecuzione giornaliera di un processo.  
  
 **Ogni**  
 Consente di impostare il numero di ore o di minuti di intervallo tra un'esecuzione e l'altra.  
  
 **Data inizio**  
 Consente di impostare la data iniziale di validità per la pianificazione.  
  
 **Data fine**  
 Consente di impostare la data finale di validità per la pianificazione.  
  
 **Nessuna data di fine**  
 Consente di specificare una validità illimitata per la pianificazione.  
  
### <a name="one-time-schedule-types-options"></a>Opzioni relative ai tipi di pianificazione da eseguire una sola volta  
 Se si pianifica una singola esecuzione per un processo, è necessario selezionare una data e un'ora nel futuro.  
  
 **Data**  
 Selezionare la data di esecuzione del processo.  
  
 **Time**  
 Selezionare l'ora di esecuzione del processo.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="summary-page"></a><a name="Summary"></a> Pagina Riepilogo  
 Usare la pagina **Riepilogo** per verificare le opzioni selezionate nelle pagine precedenti.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
 **Controlla selezioni**  
 Consente di visualizzare le opzioni selezionate in ogni pagina della procedura guidata. Fare clic su un nodo per espandere e visualizzare le opzioni selezionate in precedenza.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
##  <a name="progress-page"></a><a name="Progress"></a> Pagina Stato  
 Usare la pagina **Stato** per monitorare le informazioni sullo stato delle azioni eseguite nella **Gestione guidata partizione**. A seconda delle opzioni selezionate nella procedura guidata, la pagina **Stato** può contenere una o più azioni. Nella casella superiore viene visualizzato lo stato complessivo della procedura guidata e viene indicato il numero di messaggi di stato, di errore e di avviso restituiti durante l'esecuzione della procedura guidata.  
  
### <a name="options"></a>Opzioni  
 **Dettagli**  
 Consente di visualizzare i messaggi di azione, di stato e di altro tipo restituiti dall'azione eseguita nella procedura guidata.  
  
 **Azione**  
 Specifica il tipo e il nome di ciascuna azione.  
  
 **Status**  
 Indica se l'intera azione della procedura guidata ha restituito il valore **Esito positivo** o **Esito negativo**.  
  
 **Messaggio**  
 Fornisce tutti i messaggi di errore o di avviso restituiti dal processo.  
  
 **Stop**  
 Consente di arrestare l'azione della procedura guidata.  
  
 **Report**  
 Consente di creare un report contenente i risultati della **Gestione guidata partizione**. Le opzioni disponibili sono le seguenti:  
  
-   **Visualizza report**  
  
-   **Salva report su file**  
  
-   **Copia report negli Appunti**  
  
-   **Invia report per posta elettronica**  
  
 **Visualizza report**  
 Consente di aprire la finestra di dialogo **Visualizza report** , che contiene un report di testo dello stato della **Gestione guidata partizione**.  
  
 **Close**  
 Consente di chiudere la procedura guidata.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [In questa sezione](#Top)  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici partizionati](../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
