---
title: Creare una sessione eventi estesi utilizzando la procedura guidata (Esplora oggetti) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- Sql12.ssms.XeWizard.Summary.f1
- Sql12.ssms.XeWizard.SetSessionProperties.f1
- Sql12.ssms.XeWizard.CaptureAddFields.f1
- Sql12.ssms.XeWizard.SelectEvents.f1
- Sql12.ssms.XeWizard.SpecifySessionTargets.f1
- Sql12.ssms.XeWizard.Welcome.f1
- sql12.ssms.XeWizard.Welcome.f1
- Sql12.ssms.XeWizard.ChooseTemplate.f1
- Sql12.ssms.XeWizard.SetSessionEventFilters.f1
- Sql12.ssms.XeWizard.Results.f1
helpviewer_keywords:
- Sql11.ssms.XeWizard.CaptureAddFields.f1
- Sql11.ssms.XeWizard.SetSessionEventFilters.f1
- Sql11.ssms.XeWizard.SpecifySessionTargets.f1
- Sql11.ssms.XeWizard.Results.f1
- Sql11.ssms.XeWizard.ChooseTemplate.f1
- Sql11.ssms.XeWizard.SetSessionProperties.f1
- Sql11.ssms.XeWizard.Welcome.f1
- Sql11.ssms.XeWizard.Summary.f1
- Sql11.ssms.XeWizard.SelectEvents.f1
ms.assetid: 80c0456f-17c0-41d8-b2aa-502a2f3bb6de
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc69e3683656c5705e7e82df27b80a8a41cb81a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807363"
---
# <a name="create-an-extended-events-session-using-the-wizard-object-explorer"></a>Creare una sessione Eventi estesi utilizzando la procedura guidata (Esplora oggetti)
  Per consentire di selezionare e acquisire gli eventi nel server, gli eventi estesi includono una Creazione guidata nuova sessione, che consente di eseguire in modo semplificato i passaggi per la creazione di una sessione Eventi estesi. Creazione guidata nuova sessione espone la maggior parte della funzionalità di Eventi estesi. La [finestra di dialogo Nuova sessione](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md) consente inoltre di definire una sessione di Eventi estesi che acquisisce, visualizza e analizza i dati. La finestra di dialogo Nuova sessione espone tutta la funzionalità di Eventi estesi.  
  
### <a name="to-open-the-new-session-wizard"></a>Per aprire la Creazione guidata nuova sessione  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , quindi espandere **Eventi estesi**.  
  
2.  Fare clic con il pulsante destro del mouse su **Sessione**, quindi scegliere **Creazione guidata nuova sessione**.  
  
### <a name="use-the-following-new-session-wizard-pages-to-create-an-event-session"></a>Utilizzare le pagine seguenti della Creazione guidata nuova sessione per creare una sessione eventi  
  
-   [Introduzione](#BKMK_Welcome)  
  
-   [Imposta proprietà sessione](#BKMK_SetSessionProperties)  
  
-   [Scegliere il modello](#BKMK_ChooseTemplate)  
  
-   [Seleziona eventi da acquisire](#BKMK_SelectEventsToCapture)  
  
-   [Acquisisci campi globali](#BKMK_CaptureGlobalFields)  
  
-   [Imposta filtri di eventi di sessione](#BKMK_SetSessionEventFilters)  
  
-   [Specifica l'archiviazione dei dati di sessione](#BKMK_SpecifySessionDataOutput)  
  
-   [Riepilogo](#BKMK_Summary)  
  
-   [Crea sessione eventi](#BKMK_CreateEventSession)  
  
##  <a name="BKMK_Welcome"></a> Introduzione  
 Nella pagina **Introduzione** eseguire queste operazioni:  
  
-   Nella pagina **Introduzione** della Creazione guidata nuova sessione fare clic su **Avanti**.  
  
     Selezionare la casella di controllo **Non visualizzare più questa pagina** se si prevede di utilizzare la procedura guidata più volte e non si desidera leggere l'introduzione a ogni avvio della procedura.  
  
##  <a name="BKMK_SetSessionProperties"></a> Imposta proprietà sessione  
 Nella pagina **Imposta proprietà sessione** eseguire queste operazioni:  
  
-   Nella casella **Nome sessione** digitare un nome significativo per la sessione eventi.  
  
     Se si vuole avviare la sessione quando si avvia il server, selezionare la casella di controllo **Avviare la sessione eventi all'avvio del server** , quindi fare clic su **Avanti**.  
  
##  <a name="BKMK_ChooseTemplate"></a> Scegliere il modello  
 Nella pagina **Scegli modello** eseguire queste operazioni:  
  
-   Selezionare l'opzione **Usa questo modello di sessione eventi** per eseguire una selezione da un set di modelli preconfigurati progettati per i problemi comuni. Selezionare il modello che si vuole usare dall'elenco a discesa, quindi fare clic su **Avanti**.  
  
     oppure  
  
-   Selezionare l'opzione **Non usare un modello** se non si vuole usare un modello preconfigurato, quindi fare clic su **Avanti**.  
  
##  <a name="BKMK_SelectEventsToCapture"></a> Seleziona eventi da acquisire  
 Nella pagina **Seleziona eventi da acquisire** eseguire queste operazioni:  
  
1.  Selezionare gli eventi che si vuole acquisire in **Libreria di eventi**, quindi fare clic sulla freccia rivolta verso destra. È possibile selezionare più eventi in Libreria di eventi utilizzando MAIUSC+clic CTRL+clic.  
  
     È possibile scegliere come si desidera eseguire la ricerca degli eventi da acquisire nell'elenco a discesa. È ad esempio possibile cercare i nomi di evento oppure i nomi di evento e le relative descrizioni. È possibile cercare qualsiasi parola nella tabella immettendo il testo da cercare nella casella **Libreria di eventi** . Se, ad esempio, si vuole trovare l'evento **lock_acquired** , è possibile immettere **lock**o **lock acquire**.  
  
     Gli eventi selezionati vengono visualizzati nella casella **Eventi selezionati** . Per rimuovere gli eventi dalla casella **Eventi selezionati** , fare clic sulla freccia rivolta verso sinistra.  
  
2.  Dopo avere selezionato gli eventi che si vuole acquisire, fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Gli eventi del canale **Debug** sono nascosti per impostazione predefinita. Per visualizzare gli eventi di debug, selezionare **Debug** dall'elenco a discesa **Canale** .  
  
##  <a name="BKMK_CaptureGlobalFields"></a> Acquisisci campi globali  
 I campi globali (anche definiti azioni) vengono utilizzati per associare singole azioni o più azioni per gli eventi selezionati. Se è stato selezionato un modello nella pagina **Scegli modello** , tutti i campi globali definiti nel modello vengono visualizzati in questa pagina.  
  
 Nella pagina **Acquisisci campi globali** eseguire queste operazioni:  
  
-   Selezionare i campi globali che si vuole acquisire per la sessione eventi, quindi fare clic su **Avanti**.  
  
     È possibile rimuovere o aggiungere campi globali, selezionando o deselezionando la casella di controllo corrispondente.  
  
    > [!NOTE]  
    >  Le azioni selezionate vengono ordinate in base al campo **Nome** , per consentire la visualizzazione delle azioni associate in ordine alfabetico. È possibile eseguire l'ordinamento in base alla descrizione o allo stato di abilitazione/disabilitazione facendo clic sull'intestazione di colonna accanto al nome del campo.  
  
##  <a name="BKMK_SetSessionEventFilters"></a> Imposta filtri di eventi di sessione  
 È possibile applicare filtri (detti anche predicati) per limitare gli eventi che si desidera acquisire. Nella pagina **Imposta filtri di eventi di sessione** eseguire queste operazioni:  
  
1.  Se non si usa un modello preconfigurato, creare i criteri di filtro personalizzati, quindi fare clic su **Avanti**.  
  
     Se si usa un modello preconfigurato, nella sezione **Filtri nel modello (sola lettura)** vengono visualizzati i filtri già creati dal modello.  
  
2.  Nella sezione **Filtri aggiuntivi** è possibile configurare altri filtri per la sessione eventi.  
  
     I filtri configurati si applicano a tutti gli eventi selezionati. La Creazione guidata nuova sessione non supporta la configurazione di filtri per ogni singolo evento.  
  
    > [!NOTE]  
    >  Quando si configura una clausola group per il filtro, le parentesi ridondanti vengono rimosse dal filtro dopo che il risultato è stato salvato. Se, ad esempio, si crea un filtro che raggruppa **Clausola 1** e **Clausola 2**, le clausole vengono racchiuse tra parentesi. Dopo avere salvato il filtro, le parentesi ridondanti vengono rimosse. La rimozione delle parentesi non influisce sulla logica di filtro.  
  
##  <a name="BKMK_SpecifySessionDataOutput"></a> Specifica l'archiviazione dei dati di sessione  
 La pagina **Specifica l'archiviazione dei dati di sessione** consente di specificare la modalità di raccolta dei dati per l'analisi. Gli eventi estesi di SQL Server prevedono l'utilizzo di destinazioni per l'output dei dati. Le destinazioni consentono di archiviare i dati degli eventi ed eseguire azioni come la scrittura in un file e l'aggregazione dei dati degli eventi. Dopo avere stabilito la modalità di raccolta dei dati per l'analisi, nella pagina **Specifica l'archiviazione dei dati di sessione** eseguire queste operazioni:  
  
1.  Per set di dati di grandi dimensioni e per la creazione di record cronologici, selezionare la casella di controllo **Salva i dati in un file per l'analisi successiva** , quindi eseguire queste operazioni:  
  
    1.  Nella casella **Nome file sul server** immettere il percorso e il nome del file oppure fare clic su **Sfoglia** per specificare la directory del file nel server in cui si vuole salvare i dati.  
  
    2.  Nella casella **Dimensioni massime file** specificare le dimensioni massime del file da usare per la destinazione file. Se non si specifica un valore massimo, le dimensioni del file aumenteranno fino a quando il disco non è pieno. Le dimensioni predefinite del file sono di 1 gigabyte (GB).  
  
    3.  Selezionare la casella di controllo **Consenti rollover dei file** per abilitare il rollover dei file per la destinazione file.  
  
    4.  Nella casella **Numero massimo di file** specificare il numero massimo di file che si vuole mantenere nel file system.  
  
2.  Per la raccolta di dati recenti, selezionare la casella di controllo **Utilizzare solo i dati più recenti (destinazione ring_buffer)** , quindi eseguire queste operazioni:  
  
    1.  Nella casella **Numero di eventi da mantenere** immettere o selezionare il numero di eventi che si vuole mantenere usando le frecce rivolte verso l'alto e verso il basso.  
  
    2.  Nella casella **Dimensioni massime memoria buffer** specificare la quantità massima di memoria buffer da usare. Quando questo valore viene raggiunto, gli eventi esistenti vengono eliminati.  
  
    3.  Se si vuole mantenere un numero specifico di eventi di ogni tipo nel buffer, selezionare la casella di controllo **Mantenere un numero specificato di eventi (per tipo) quando il buffer è pieno** .  
  
    4.  Nella casella **Numero di eventi da mantenere (per tipo)** immettere o selezionare il numero di eventi (per tipo) che si vuole mantenere usando le frecce rivolte verso l'alto e verso il basso.  
  
##  <a name="BKMK_Summary"></a> Riepilogo  
 Nella pagina **Riepilogo** eseguire queste operazioni:  
  
1.  Verificare che le selezioni siano corrette. Espandere i nodi della sessione eventi per verificare che tutte le selezioni verranno incluse nella sessione eventi.  
  
2.  Fare clic su **Script** per esportare lo script di creazione della sessione in una nuova finestra dell'editor di query.  
  
3.  Fare clic su **Fine** per creare la sessione eventi.  
  
##  <a name="BKMK_CreateEventSession"></a> Crea sessione eventi  
 Dopo la creazione della sessione eventi, nella pagina **Crea sessione eventi** eseguire queste operazioni:  
  
1.  Fare clic su **Avviare la sessione eventi subito dopo la creazione della sessione** per avviare la sessione dopo la chiusura della procedura guidata. Per poter visualizzare i dati dinamici, è necessario avviare la sessione eventi subito dopo la creazione della sessione.  
  
2.  Fare clic su **Controllare i dati dinamici sullo schermo al momento dell'acquisizione** per visualizzare i dati dinamici per la sessione eventi. La traccia dei dati dinamici inizierà a essere visualizzata subito dopo la creazione della sessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una sessione Eventi estesi usando la finestra di dialogo Nuova sessione](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  
