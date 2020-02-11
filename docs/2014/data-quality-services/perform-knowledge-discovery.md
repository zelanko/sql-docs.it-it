---
title: Eseguire l'individuazione di informazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.kbanalyze.f1
- sql12.dqs.kb.viewselectcd.f1
- sql12.dqs.kb.kbmap.f1
- sql12.dqs.kb.kbterms.f1
ms.assetid: 34a0ea16-02e6-46ed-90bc-dede68687f63
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cc2eac8564c08831527d71ee5942c37b618aedcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481300"
---
# <a name="perform-knowledge-discovery"></a>Esecuzione dell'individuazione delle informazioni
  In questo argomento viene descritto come compilare una Knowledge Base tramite l'individuazione delle informazioni. Durante il processo di individuazione in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) vengono analizzati i dati in un'origine dati di esempio tramite un processo computerizzato e vengono aggiunte le informazioni ottenute dalla Knowledge Base. Tali informazioni possono essere modificate e migliorate nel passaggio **Gestisci valori di dominio** dell'attività di individuazione delle informazioni o nell'attività di gestione del dominio.  
  
 L'individuazione delle informazioni è un processo basato su procedure guidate che include tre passaggi, ognuno dei quali deve essere completato.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Se i dati di origine su cui viene eseguita l'individuazione si trovano in un file di Excel, è necessario che Microsoft Excel sia installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . In caso contrario, non sarà possibile selezionare il file di Excel nella fase di mapping. I file creati da Microsoft Excel potranno presentare l'estensione xlsx, xls o csv. Se viene utilizzata la versione a 64 bit di Excel, sono supportati solo i file di Excel 2003 (xls), mentre non sono supportati file di Excel 2007 o 2010 (xlsx). Se si utilizza una versione a 64 bit di Excel 2007 o 2010, salvare il file come file xls o csv o installare una versione a 32 bit di Excel.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN per creare una Knowledge Base.  
  
##  <a name="FirstStep"></a>Primo passaggio: avviare l'individuazione delle informazioni  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Se si desidera eseguire l'individuazione delle informazioni in una nuova Knowledge Base, fare clic su **Nuova Knowledge Base**, immettere il nome e la descrizione e, se applicabile, specificare l'oggetto da cui si crea la Knowledge Base. Se si desidera eseguire l'individuazione delle informazioni in una Knowledge Base esistente, fare clic su **Apri Knowledge Base**, quindi seleziona una Knowledge Base.  
  
3.  Selezionare **Individuazione informazioni** come attività, quindi fare clic su **Crea** per creare la nuova Knowledge Base, oppure **Apri** per aprirne una esistente.  
  
##  <a name="Mapping"></a>Fase di mapping  
  
1.  Nel campo **Origine dati** selezionare **SQL Server** (valore predefinito) o **File di Excel**.  
  
    > [!NOTE]  
    >  In questa pagina è possibile creare una connessione a un'origine dati SQL Server o Excel, quindi viene eseguito il mapping tra le colonne nell'origine dati e un dominio nella Knowledge Base. Nella tabella Mapping vengono visualizzate tutte le colonne nel database di origine che verrà analizzato per aggiungere informazioni ai domini corrispondenti. Vengono eseguiti mapping tra le colonne nell'origine dati e un dominio nella Knowledge Base.  
  
2.  Se l'origine dati è **SQL Server**, procedere come segue:  
  
    1.  Nel campo **Database** selezionare il database di origine che si desidera analizzare per creare la Knowledge Base. Nella casella di testo a discesa verranno elencati i database disponibili. Il database di origine deve trovarsi nella stessa istanza di SQL Server di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], in caso contrario, non verrà visualizzato nell'elenco a discesa.  
  
    2.  Nel campo **Tabella/Vista** selezionare la tabella o la vista che si desidera analizzare per creare la Knowledge Base. Questa tabella o vista deve essere costituita da dati di esempio, non da un intero database di origine su cui viene eseguita la pulizia o l'individuazione di corrispondenze dei dati. Nella casella di testo a discesa verranno elencate le tabelle e le viste disponibili per il database selezionato.  
  
3.  Se l'origine dati è **Excel**, procedere come segue:  
  
    1.  Fare clic su **Sfoglia** e selezionare il file di Excel che si desidera analizzare per creare la Knowledge Base. Per selezionare un file di Excel, è necessario che Excel sia installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Se Excel non è installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , il pulsante Sfoglia non sarà disponibile e verrà visualizzata una notifica sotto questa casella di testo in cui si avvisa che Excel non è installato.  
  
    2.  Selezionare la casella di controllo **Utilizza la prima riga come intestazione** se la prima riga del file di Excel contiene dati di intestazione.  
  
4.  Nella tabella **Mapping** eseguire il mapping di ogni colonna di origine su cui si desidera eseguire l'individuazione delle informazioni a un dominio nella Knowledge Base, come segue:  
  
    1.  Creare un mapping selezionando una colonna di origine nell'elenco a discesa per la **Colonna di origine** di una riga vuota, quindi selezionando un dominio nell'elenco a discesa per la colonna **Dominio** nella stessa riga, se esiste un dominio. Se non esiste alcun dominio, fare clic su **Crea un dominio** o **Crea un dominio composito** per crearne uno. Per ulteriori informazioni, vedere [Creare una regola di dominio](../../2014/data-quality-services/create-a-domain-rule.md) o [Crea un dominio composito](../../2014/data-quality-services/create-a-composite-domain.md).  
  
    2.  Ripetere il passaggio precedente per ogni mapping. Per modificare il numero di righe nella tabella, fare clic su **Aggiungi un mapping colonne**o selezionare una riga e fare clic su **Rimuovi mapping colonne selezionate**. Se si fa clic su **Rimuovi mapping colonne selezionate** quando è selezionata una riga popolata, la riga selezionata verrà eliminata anche se è presente una riga non popolata.  
  
        > [!NOTE]  
        >  È possibile eseguire il mapping dei dati di origine a un dominio DQS per eseguire l'individuazione di informazioni solo se il tipo di dati di origine è supportato in DQS e corrisponde al tipo di dati del dominio DQS. Per ulteriori informazioni sui tipi di dati supportati, vedere [Tipi di dati di SQL Server e SSIS supportati per i domini DQS](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
    3.  Fare clic su **Visualizza/Seleziona domini compositi** per visualizzare i domini compositi definiti. Se non è stato definito alcun dominio composito, il controllo non sarà disponibile.  
  
    4.  Fare clic su **Anteprima origine dati** per visualizzare in una finestra popup tutti i dati dell'origine dati selezionata nella casella di testo **Tabella/Vista** o **File di Excel** .  
  
5.  Fare clic su **Avanti** per passare alla pagina **Individua** della procedura guidata Individuazione informazioni. È inoltre possibile selezionare le opzioni seguenti:  
  
    -   Fare clic su **Annulla** per terminare l'attività di individuazione delle informazioni. Il lavoro verrà perso e sarà visualizzata di nuovo la home page di DQS.  
  
    -   Fare clic su **Chiudi** per salvare il lavoro e tornare alla home page di DQS. La Knowledge Base verrà bloccata e lo stato della Knowledge Base nella relativa tabella della schermata **Apri Knowledge Base** sarà **Individuazione - Mapping**. Dopo avere fatto clic su **Chiudi**per eseguire l'attività Gestione dominio è necessario fare clic su **Individuazione informazioni** nella schermata **Apri Knowledge Base** , passare alla schermata **Gestione Knowledge Base: Gestisci termini di dominio** , fare clic su **Fine**, quindi fare clic su **Sì** per pubblicare la Knowledge Base o su **No** per salvare il lavoro nella Knowledge Base e uscire.  
  
##  <a name="Discover"></a>Fase di individuazione  
  
1.  Fare clic su **Avvia** per analizzare l'origine dati.  
  
    > [!NOTE]  
    >  L'individuazione viene eseguita sulle colonne immesse nella tabella **Mapping** della pagina **Mappa** . Il dominio di cui è stato eseguito il mapping a ogni colonna verrà popolato con le informazioni ricavate dall'individuazione. Se il dominio è un dominio composito, le informazioni verranno aggiunte ai singoli domini singoli da cui è costituito il dominio composito.  
  
2.  Durante l'esecuzione del processo di individuazione, controllare lo stato di completamento visualizzato per ogni passaggio dell'individuazione: **Pre-elaborazione record**, **Esecuzione regole di dominio**ed **Esecuzione individuazione**. La percentuale e lo stato di completamento verranno visualizzati per ognuna di queste fasi.  
  
3.  Al termine dell'analisi, verificare che la riga di stato sotto le statistiche di completamento indichi che l'operazione sia stata completata correttamente.  
  
    > [!NOTE]  
    >  Se si esce dalla schermata prima della fine del caricamento del file, il processo di caricamento verrà terminato.  
  
4.  Dopo il completamento dell'analisi, verificare le statistiche nella scheda **Profiler** per controllare lo stato dei dati. Per altre informazioni, vedere **Data Profiling and Notifications in DQS**.  
  
5.  Una volta completata l'analisi, il pulsante **Avvia** viene sostituito dal pulsante **Riavvia** . Fare clic su **Riavvia** per eseguire di nuovo il processo di analisi. Se i risultati dall'analisi precedente non sono stati ancora salvati, facendo clic su **Riavvia** si causerà la perdita di tali dati non salvati. Per continuare, fare clic su **Sì** nella finestra popup. Durante l'esecuzione dell'analisi, non lasciare la pagina o il processo di analisi verrà interrotto.  
  
6.  Fare clic su **Avanti** per passare alla pagina **Gestisci valori di dominio** della procedura guidata Individuazione informazioni. In questa pagina è possibile modificare le informazioni aggiunte ai domini della Knowledge Base. È inoltre possibile selezionare le opzioni seguenti:  
  
    -   Fare clic su **Annulla** per terminare l'attività di individuazione delle informazioni. Il lavoro verrà perso e sarà visualizzata di nuovo la home page di DQS.  
  
    -   Fare clic su **Chiudi** per salvare il lavoro e tornare alla home page di DQS. La Knowledge Base verrà bloccata e lo stato della Knowledge Base nella relativa tabella della schermata **Apri Knowledge Base** sarà **Individuazione informazioni - Individua**. Dopo avere fatto clic su **Chiudi**per eseguire l'attività Gestione dominio è necessario fare clic su **Individuazione informazioni** nella schermata **Apri Knowledge Base** , passare alla schermata **Gestione Knowledge Base: Gestisci termini di dominio** , fare clic su **Fine**, quindi fare clic su **Sì** per pubblicare la Knowledge Base o su **No** per salvare il lavoro nella Knowledge Base e uscire.  
  
    -   Fare clic per tornare alla pagina **Individua** .  
  
##  <a name="Manage"></a>Fase di gestione dei risultati di individuazione dati  
 Dopo avere eseguito l'attività di individuazione delle informazioni, è possibile modificare i valori come segue:  
  
-   Aggiungere un valore di dominio all'elenco di valori o selezionare un valore ed eliminarlo dall'elenco  
  
-   Modificare lo stato di un valore di dominio rispetto a come viene definito dal processo di individuazione DQS, impostandolo come corretto, in errore o non valido  
  
-   Immettere un valore di sostituzione per un valore in errore o non valido  
  
-   Impostare due o più valori come sinonimi e modificare il valore iniziale rispetto a come è stato impostato dal processo di individuazione, in modo che il valore iniziale sostituisca il valore del sinonimo, se durante la creazione del dominio è stata impostata la proprietà **Utilizza valori iniziali**  
  
-   Importare i valori di dominio da un file di Excel  
  
 Nella tabella **Valore** vengono visualizzate le informazioni aggiunte alla Knowledge Base per un singolo dominio. Selezionare tale dominio nell'elenco di domini del riquadro a sinistra. Le colonne del campo sono le seguenti:  
  
-   Nella colonna **Valore** vengono visualizzati tutti i valori aggiunti dal processo di individuazione al dominio selezionato da un campo nei dati di esempio. Qualsiasi valore indicato come in errore verrà visualizzato come sinonimo di un valore indicato come corretto.  
  
-   Nella colonna **Frequenza** viene visualizzato il numero di istanze del valore nel campo del database di esempio a cui è stato eseguito il mapping del dominio. Per un dominio composito, vengono visualizzati solo i valori con una frequenza maggiore o uguale a 20. I dati relativi alla frequenza sono disponibili in quanto il processo di individuazione delle informazioni dispone ancora di una connessione al database di esempio. I dati relativi alla frequenza non sono disponibili nella tabella di dominio nella scheda Valori di dominio della schermata Gestione dominio in quanto il processo di gestione del dominio non dispone di una connessione al database di esempio.  
  
-   Nella colonna **Tipo** viene visualizzato lo stato del valore, come determinato dal processo di individuazione. Un segno di spunta verde indica che il valore è corretto o che sono state apportate correzioni, una croce rossa indica che il valore è in errore, mentre un triangolo arancione con un punto esclamativo indica che il valore non è valido. Un valore non valido non è conforme ai requisiti dei dati per il dominio. Un valore in errore può essere valido, ma non è il valore corretto per la finalità dei dati.  
  
-   Nella colonna **Correggi in** viene visualizzato il valore corretto in cui verrà modificato il valore originale, contrassegnato come in errore o non valido. Il valore corretto viene proposto da DQS come risultato del processo di individuazione.  
  
 Gestire i risultati dell'individuazione come segue:  
  
1.  Nel riquadro **Elenco di domini** a sinistra selezionare un dominio per cui impostare i valori di dominio. Per modificare i valori visualizzati, è possibile effettuare le operazioni seguenti.  
  
    -   Visualizzare i risultati desiderati nella tabella, in base al relativo stato, selezionando lo stato nell'elenco **Filtro** .  
  
    -   Trovare i dati che si desidera controllare o modificare immettendo una o più lettere da cercare nella casella di testo Trova. Tali lettere verranno evidenziate in tutti i valori visualizzati.  
  
    -   Fare clic su **Mostra solo nuovi** per limitare i valori visualizzati nella tabella solo ai valori individuati nella sessione corrente, non nelle sessioni precedenti.  
  
    -   Fare clic sul pulsante **Espandi tutto** per visualizzare tutti i valori in qualsiasi gruppo di sinonimi quando lo stato corrente è compresso o il pulsante **Comprimi tutto** per nascondere tutto tranne il valore iniziale in qualsiasi gruppo di sinonimi quando lo stato corrente è espanso.  
  
    -   Fare clic sul pulsante **Mostra/Nascondi il pannello della cronologia delle modifiche dei valori di dominio** per visualizzare un'anteprima popup nella parte inferiore della tabella dei valori in cui vengono mostrate le modifiche recenti alla raccolta dei valori di dominio.  
  
2.  Trovare tutte le correzioni proposte da Data Quality Services impostando **Filtro** su **Errori**. Verificare che il valore sia effettivamente in errore e che il valore nella colonna **Correggi in** sia appropriato.  
  
3.  Impostare **Filtro** su **Tutti i valori** e verificare che lo stato dei valori sia appropriato. Per modificare lo stato di un valore, selezionare il valore e quindi fare clic sul pulsante **Imposta i valori di dominio selezionati come corretti** (segno di spunta), sul pulsante **Imposta i valori di dominio selezionati come errori** (croce) o sul pulsante **Imposta i valori di dominio selezionati come non validi** (triangolo).  
  
4.  Per modificare lo stato di un valore, procedere come segue:  
  
    1.  **Imposta i valori di dominio selezionati come corretti**: per modificare lo stato di un valore da errore o non valido a corretto, selezionare il valore, quindi fare clic su **imposta i valori di dominio selezionati come corretti** (segno di spunta) dalla freccia in giù nella barra delle icone o dall'elenco a discesa tipo. Se il valore in errore o non valido viene raggruppato con un valore corretto, eliminare il valore dopo l'operazione.  
  
    2.  **Imposta i valori di dominio selezionati come errori**: per modificare lo stato di un valore da corretto o non valido in errore, selezionare il valore, quindi fare clic sull'icona **imposta i valori di dominio selezionati come errori** (Croce) dalla freccia in giù nella barra delle icone o dall'elenco a discesa tipo. È possibile immettere una correzione nella colonna **Correggi in** o lasciarla vuota.  
  
    3.  **Imposta i valori di dominio selezionati come non validi**: per modificare lo stato di un valore da corretto o da errore a non valido, selezionare il valore, quindi fare clic sull'icona **imposta i valori di dominio selezionati come non validi** (triangolo) dalla freccia in giù nella barra delle icone o dall'elenco a discesa tipo. È possibile immettere una correzione nella colonna **Correggi in** o lasciarla vuota.  
  
    4.  **Correggi**in: dopo avere impostato un valore come in errore o non valido, immettere un nuovo valore nella colonna **Correggi** in. In DQS verrà aggiunta una nuova riga per il valore sostitutivo che verrà designato come valore corretto, quindi verranno raggruppati i due valori. Il nuovo valore verrà visualizzato come valore iniziale, con il valore iniziale in grassetto e il valore in errore o non valido rientrato.  
  
5.  Per designare i valori come gruppo di sinonimi, selezionare più valori corretti, quindi procedere come segue:  
  
    -   **Imposta i valori di dominio selezionati come sinonimi**: fare clic per impostare i valori selezionati come sinonimi. In DQS uno dei valori verrà definito come valore iniziale con cui verranno sostituiti gli altri valori.  
  
        > [!NOTE]  
        >  Se si selezionano due o più valori in un gruppo e un altro valore all'esterno del gruppo e quindi si impostano come sinonimi, verrà generato un messaggio di errore non corretto. Dopo avere chiuso la finestra popup del messaggio di errore, i valori verranno impostati correttamente come sinonimi.  
  
    -   **Interrompi relazione tra sinonimi selezionati**: fare clic per annullare la designazione del sinonimo.  
  
    -   **Imposta valore di dominio selezionato come valore principale del gruppo**: modificare il valore di riferimento del gruppo selezionando un valore nel gruppo non designato come valore principale, quindi facendo clic sul pulsante **Imposta valore di dominio selezionato come valore principale del** gruppo.  
  
6.  **Correttore ortografico**: se è stato abilitato il correttore ortografico nella pagina Proprietà dominio, trovare tutti i valori con una sottolineatura rossa ondulata, l'indicazione che il correttore ortografico sta suggerendo una correzione. Fare clic con il pulsante destro del mouse sul valore con la sottolineatura e selezionare una correzione, se appropriata. Il tipo di valore diventa (o rimane) in errore e la correzione verrà aggiunta alla colonna **Correggi in** . Fare clic sulla freccia in giù per visualizzare ulteriori correzioni proposte. Immettere una correzione manualmente per aggiungerla al dizionario del Correttore ortografico e poterla selezionare come correzione. Per ulteriori informazioni, vedere [Utilizzare il correttore ortografico DQS](../../2014/data-quality-services/use-the-dqs-speller.md) e [Imposta proprietà del dominio](../../2014/data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Per utilizzare il Correttore ortografico, è possibile abilitarlo nella pagina **Proprietà dominio** o, se è disabilitato nella pagina **Proprietà dominio** , è possibile fare clic sull'icona **Abilita/Disabilita correttore ortografico** nella pagina **Gestisci risultati individuazione dati** per abilitarlo in questa pagina.  
  
7.  **Aggiungi nuovo valore di dominio**: aggiungere un nuovo valore al dominio facendo clic sul pulsante **Aggiungi nuovo valore di dominio** per aggiungere una riga alla fine della tabella. Dopo avere immesso un valore, la riga verrà riposizionata in ordine alfabetico.  
  
8.  **Importare i valori di dominio da Excel**: aggiungere nuovi valori da un foglio di calcolo di Excel facendo clic sulla freccia in giù per l'icona **Importa valori** , quindi selezionando **Importa valori di dominio da Excel**. Immettere il nome file, selezionare **Utilizza la prima riga come intestazione** se appropriato, quindi fare clic su **OK**. Per altre informazioni, vedere [Importare i valori da un file di Excel in un dominio](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
9. **Importa valori progetto**: aggiungere nuovi valori da un progetto Data Quality facendo clic sulla freccia in giù per l'icona **Importa valori** , quindi selezionando **Importa valori progetto**. Immettere il nome file, selezionare **Utilizza la prima riga come intestazione** se appropriato, quindi fare clic su **OK**. Selezionare il progetto da cui si desidera importare i valori, quindi fare clic su **OK**. Verranno visualizzati i valori importati. Fare clic su **Fine**. Per ulteriori informazioni, vedere Importare i valori di progetto in un dominio.  
  
10. **Elimina valori di dominio selezionati**: rimuovere uno o più valori esistenti dal dominio selezionando i valori, quindi facendo clic sul pulsante Elimina valori di **dominio selezionati** . Non è possibile eliminare il valore DQS_NULL, pertanto se si scelgono più valori da eliminare e il valore DQS_NULL è tra questi, l'operazione non riuscirà.  
  
11. Fare clic su **Fine** per completare l'attività di individuazione delle informazioni. Se non sono stati controllati tutti i domini, verrà visualizzata una finestra popup. Fare clic su **Sì** per continuare il controllo o su **No** per procedere. Se si fa clic su NO, verrà visualizzata un'altra finestra popup con le opzioni seguenti:  
  
    1.  **Publish**: la Knowledge base verrà pubblicata per l'uso da parte dell'utente corrente o di altri utenti. La Knowledge Base non verrà bloccata, lo stato della Knowledge Base nella relativa tabella verrà impostato come vuoto e saranno disponibili entrambe le attività, Gestione dominio e Individuazione informazioni. Verrà di nuovo visualizzata la home page. Per completare il processo, fare clic su **Sì** nella finestra popup.  
  
    2.  **No**: il lavoro verrà salvato, la Knowledge base rimarrà bloccata e lo stato della Knowledge base verrà impostato su in lavorazione. Entrambe le attività Gestione dominio e Individuazione informazioni saranno disponibili. Verrà di nuovo visualizzata la home page.  
  
    3.  **Annulla**: la finestra popup verrà chiusa e si rimarrà nella pagina **Gestisci valori di dominio** .  
  
12. È inoltre possibile fare clic sulle opzioni seguenti:  
  
    -   **Annulla** per terminare l'attività di individuazione delle informazioni, perdere il lavoro e tornare al Home page DQS.  
  
    -   **Close** per tornare al Home page DQS mentre si salva il lavoro. La Knowledge Base verrà bloccata e lo stato della Knowledge Base nella relativa tabella della schermata **Apri Knowledge Base** sarà **Discovery - Value Management** (Individuazione - Gestione valore).  
  
    -   Fare clic su **Indietro** per tornare alla pagina **Individua** . Dopo avere fatto clic su **Chiudi**per eseguire l'attività Gestione dominio è necessario fare clic su **Individuazione informazioni** nella schermata **Apri Knowledge Base** , passare alla schermata **Gestione Knowledge Base: Gestisci termini di dominio** , fare clic su **Fine**, quindi fare clic su **Sì** per pubblicare la Knowledge Base o su **No** per salvare il lavoro nella Knowledge Base e uscire.  
  
##  <a name="FollowUp"></a>Completamento: fasi successive all'esecuzione dell'individuazione delle informazioni  
 Dopo avere aggiunto le informazioni alla Knowledge Base nel processo computerizzato di individuazione delle informazioni, è possibile utilizzare immediatamente la Knowledge Base per un progetto di pulizia o è possibile eseguire un'attività di gestione del dominio prima di eseguirne la pulizia. Per altre informazioni sulla pulizia dei dati o sulla gestione del dominio, vedere [Pulizia dei dati](../../2014/data-quality-services/data-cleansing.md) o [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md).  
  
##  <a name="Meaning"></a>Il significato dei valori corretti, errori e non validi  
 A ogni valore nella tabella **Valore** della pagina **Valori di dominio** è assegnata un'impostazione **Tipo** di **Corretti**, **Errori**o **Non validi**. Il tipo del valore viene generato inizialmente dall'attività di individuazione delle informazioni ma è possibile modificarlo nel modo desiderato. Il tipo finale, basato sia sulle modifiche di individuazione che su quelle interattive, viene generato dall'attività di pulizia. Le impostazioni hanno il significato seguente:  
  
-   **Corretto:** Si tratta di un valore che appartiene al dominio e non contiene errori di sintassi. Ad esempio, "Chicago" in un dominio Città è corretto.  
  
-   **Errore:** Si tratta di un valore che appartiene al dominio, ma non è un valore corretto. Ad esempio, "Shicago" anziché "Chicago" in un dominio Città è un errore. In DQS un valore viene definito come in errore quando nel processo di individuazione vengono rilevati un errore di sintassi e una correzione associata. Gli errori di sintassi includono gli errori di ortografia.  
  
-   **Non valido:** Si tratta di un valore che non appartiene al dominio e non dispone di una correzione. Ad esempio, il valore "12345" in un dominio Città non è valido. In DQS un valore viene definito come non valido quando non supera una regola di dominio.  
  
 È possibile modificare manualmente l'impostazione Tipo scegliendo uno degli altri due valori. In DQS non viene applica la semantica della validità e dell'errore nelle operazioni manuali. È possibile immettere una correzione per un valore Non validi senza modificarne lo stato. È possibile definire un valore come non valido anche se ha superato una regola di dominio. È possibile definire un valore come in errore anche se il processo di individuazione non ha rilevato un errore di sintassi. È inoltre possibile rimuovere una correzione a un valore Errori, contrassegnato come Corretti, senza modificarne lo stato.  
  
 Quando si esegue la pulizia interattiva dei dati nella pagina **Gestisci e visualizza risultati** dell'attività **Pulizia** , nella scheda **Non validi** della pagina **Gestisci e visualizza risultati** vengono inclusi sia i valori in errore che quelli non validi.  
  
##  <a name="Display"></a>Come visualizzare i valori appropriati  
 È possibile modificare la visualizzazione come segue:  
  
-   **Filtrare** i risultati desiderati nella tabella, in base al relativo stato, selezionando lo stato nell'elenco a discesa **filtro** .  
  
-   **Trovare** i dati che si desidera controllare o modificare immettendo una o più lettere da cercare nella casella di testo **trova** . Tali lettere verranno evidenziate in tutti i valori visualizzati.  
  
-   Fare clic su **Mostra solo nuovi** per limitare i valori visualizzati nella tabella solo ai valori individuati nella sessione corrente, non nelle sessioni precedenti.  
  
-   Fare clic sul pulsante **Espandi tutto** per visualizzare tutti i valori in qualsiasi gruppo di sinonimi quando lo stato corrente è compresso.  
  
-   Fare clic sul pulsante **Comprimi tutto** per nascondere tutto tranne il valore iniziale in qualsiasi gruppo di sinonimi quando lo stato corrente è espanso.  
  
-   Fare clic sul pulsante **Mostra/Nascondi il pannello della cronologia delle modifiche dei valori di dominio** per visualizzare un'anteprima popup nella parte inferiore della tabella dei valori in cui vengono mostrate le modifiche recenti alla raccolta dei valori di dominio.  
  
##  <a name="Profiler"></a>Statistiche Profiler  
 Nella scheda Profiler sono fornite statistiche tramite cui viene indicata la qualità dei dati di origine. Le statistiche non misurano la qualità della Knowledge Base. Il profiling nell'individuazione informazioni fornisce informazioni essenziali quanto a completezza e univocità ma non misura l'accuratezza. Il profiling per la gestione delle informazioni consente di valutare l'importanza dell'origine dati per la compilazione e il miglioramento delle informazioni in una Knowledge Base.  
  
 La scheda **Profiler** fornisce le statistiche seguenti per il processo di individuazione, per campo e dominio:  
  
-   **Record**: numero di record individuati nel campione di dati  
  
-   **Valori totali**: numero di valori totali trovati per ogni campo e in totale  
  
-   **Nuovi valori**: numero di valori totali per ogni campo e per tutti i campi di cui è stato eseguito il mapping nuovi rispetto all'ultimo processo di individuazione e relativa percentuale dei valori totali  
  
-   **Valori univoci**: numero di valori totali per ogni campo e per tutti i campi di cui è stato eseguito il mapping e relativa percentuale dei valori totali  
  
-   **Nuovi valori univoci**: numero di valori univoci per ogni campo e per tutti i campi di cui è stato eseguito il mapping nuovi dall'ultimo processo di individuazione e percentuale dei valori totali  
  
-   **Valido nei valori di dominio**: numero di valori totali per ogni campo e per tutti i campi mappati validi e relativa percentuale dei valori totali  
  
 Le statistiche relative ai campi includono:  
  
-   **Field**: nome del campo nel database di origine  
  
-   **Dominio**: nome del dominio di cui viene eseguito il mapping al campo  
  
-   **Nuovo**: numero di nuovi valori e percentuale di nuovi valori rispetto ai valori esistenti nel campo  
  
-   **Unique**: numero di record univoci nel campo e relativa percentuale del totale  
  
-   **Valido nel dominio**: numero di valori di dominio validi e relativa percentuale del totale  
  
-   **Completezza**: la completezza di ogni campo di origine di cui è stato eseguito il mapping per l'esercizio corrispondente  
  
 Il profiling nell'individuazione informazioni fornisce informazioni essenziali quanto a completezza. Se il profiling suggerisce che un campo è relativamente incompleto, è necessario rimuoverlo dalla Knowledge Base di un progetto Data Quality. È possibile che il profiling non fornisca statistiche di completezza affidabili per i domini compositi. Se sono necessarie statistiche di completezza, utilizzare domini singoli anziché domini compositi. Se si desidera utilizzare domini compositi, è consigliabile creare una Knowledge Base con domini singoli di cui eseguire il profiling per determinare la completezza, quindi creare un altro dominio con un dominio composito per il processo di pulizia. Ad esempio, il profiling potrebbe mostrare una completezza del 95% per record relativi a indirizzi, utilizzando un dominio composito, ma potrebbe esservi un livello di incompletezza molto più alto per una delle colonne, ad esempio una colonna relativa al codice postale (CAP). In questo esempio, è necessario misurare la completezza della colonna del CAP con un solo dominio. Il profiling fornirà probabilmente statistiche di accuratezza affidabili per i domini compositi perché è possibile misurare l'accuratezza di più colonne allo stesso tempo. Il valore di questi dati sta nell'aggregazione composta, pertanto è consigliabile misurarne l'accuratezza con un dominio composito.  
  
 Le statistiche vengono visualizzate nella scheda Profiler nelle fasi seguenti:  
  
-   Nella fase **Pre-elaborazione record** in DQS vengono caricati i dati e indicizzati. Tale operazione viene eseguita un record alla volta o un batch alla volta, pertanto lo stato di avanzamento può essere visualizzato per record. Durante l'esecuzione di questo passaggio può essere generata la maggior parte dei dati di profiling, ad eccezione dei valori **Valido nel dominio** .  
  
-   Nella fase **Esecuzione regole di dominio** la colonna **Valido nel dominio** viene popolata non appena le regole di dominio vengono tutte eseguite come unità atomica di ogni valore di dominio.  
  
-   Nella fase di **individuazione in esecuzione** non vengono aggiornati nuovi dati nella scheda Profiler. Eventuali errori di sintassi rilevati possono essere visualizzati nel passaggio successivo della procedura guidata, la fase **Gestisci valori di dominio** .  
  
 Per l'attività di individuazione delle informazioni, le condizioni seguenti generano notifiche:  
  
-   Non sono presenti nuovi valori in un campo. È consigliabile eliminarlo dal mapping.  
  
-   Sono presenti alcuni valori nuovi in un campo. È possibile eliminarlo dal mapping.  
  
-   Un campo è vuoto. È consigliabile eliminarlo dal mapping.  
  
-   Il punteggio di completezza del campo è molto basso; è consigliabile eliminarlo dal mapping.  
  
-   Un campo contiene solo valori non validi; è necessario verificare il mapping e la rilevanza delle regole di dominio sul contenuto del campo.  
  
-   Un campo contiene un basso livello di valori validi; è necessario verificare il mapping e la rilevanza delle regole di dominio sul contenuto del campo.  
  
 Per ulteriori informazioni sul profiling, vedere [Profiling di dati e notifiche in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  
