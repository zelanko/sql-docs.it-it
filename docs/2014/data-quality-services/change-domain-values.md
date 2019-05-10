---
title: Modificare i valori di dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.values.f1
ms.assetid: 8c90ab70-3aea-4eaf-a174-4159485c87d3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 111b4dc0c1731b28da503794008be2b4d269094f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65481127"
---
# <a name="change-domain-values"></a>Modificare i valori di dominio
  In questo argomento viene descritto come modificare e aumentare i metadati in una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Dopo avere generato le informazioni mediante l'individuazione delle informazioni, importato le informazioni nella Knowledge Base o nei domini oppure basato una Knowledge Base su un'altra Knowledge Base, è possibile modificare in modo interattivo i valori dei dati. La generazione della Knowledge Base non solo sfrutta i processi computerizzati, ma consente di utilizzare informazioni personalizzate per verificare i valori dei dati e modificarli nei modi seguenti:  
  
-   Aggiungere un valore di dominio all'elenco di valori o selezionare un valore ed eliminarlo dall'elenco  
  
-   Modificare lo stato di un valore di dominio rispetto a come viene definito dal processo di individuazione DQS, impostandolo come corretto, in errore o non valido  
  
-   Immettere un valore di sostituzione per un valore in errore o non valido. Un valore è non valido se non fa parte del dominio, ad esempio se non è conforme al tipo di dati del dominio o non supera una regola di dominio. Un valore è in errore se fa parte del dominio, ma contiene un errore di sintassi.  
  
-   Impostare due o più valori come sinonimi e modificare il valore iniziale rispetto a come è stato impostato dal processo di individuazione, in modo che il valore iniziale sostituisca il valore del sinonimo, se durante la creazione del dominio è stata impostata la proprietà **Utilizza valori iniziali**  
  
-   Importare i valori di dominio da un file di Excel  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per modificare un valore di dominio, è necessario disporre di una Knowledge Base e di un dominio aperto nell'attività Gestione dominio.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per modificare i valori di dominio, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Change"></a> Modificare i valori di dominio  
 Nella tabella **Valore** vengono visualizzate le informazioni aggiunte alla Knowledge Base per un singolo dominio. È possibile selezionare un dominio diverso nell'elenco di domini in qualsiasi momento per visualizzare i valori di tale dominio. Le colonne del campo sono le seguenti:  
  
-   Nella colonna **Valore** vengono visualizzati tutti i valori aggiunti dal processo di individuazione al dominio selezionato da un campo nei dati di esempio. Qualsiasi valore indicato come in errore verrà visualizzato come sinonimo di un valore indicato come corretto.  
  
-   Nella colonna **Tipo** viene visualizzato lo stato del valore, come determinato dal processo di individuazione. Un segno di spunta verde indica che il valore è corretto o che sono state apportate correzioni, una croce rossa indica che il valore è in errore, mentre un triangolo arancione con un punto esclamativo indica che il valore non è valido. Un valore non valido non è conforme ai requisiti dei dati per il dominio. Un valore in errore può essere valido, ma non è il valore corretto per la finalità dei dati.  
  
-   Nella colonna **Correggi in** viene visualizzato il valore corretto in cui verrà modificato il valore originale, contrassegnato come in errore o non valido. Il valore corretto viene proposto da DQS come risultato del processo di individuazione.  
  
 Per modificare i valori, procedere come segue:  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire o creare una Knowledge Base. Selezionare **Gestione dominio** come attività, quindi fare clic su **Apri** o **Crea**. Per ulteriori informazioni, vedere [Creare una Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md) o [Apertura di una Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La gestione del dominio viene eseguita in una pagina del client Data Quality Services che contiene cinque schede per le operazioni di gestione del dominio separate. Non si tratta di un processo basato su procedure guidate. Ciascuna operazione di gestione può essere eseguita separatamente.  
  
3.  **Dall'elenco di domini** nella pagina **Gestione dominio** selezionare il dominio per il quale si desidera modificare i valori o creare un nuovo dominio. Se è necessario creare un nuovo dominio, vedere [Crea un dominio](../../2014/data-quality-services/create-a-domain.md). Fare clic sulla scheda **Valori di dominio** .  
  
4.  Visualizzare i valori che è necessario modificare nella tabella **Valore** . Per altre informazioni, vedere [Modalità di visualizzazione dei valori appropriati](#Display) più avanti.  
  
5.  Per modificare lo stato di un valore, procedere come segue:  
  
    -   **Imposta i valori di dominio selezionati come corretti**: per modificare lo stato di un valore da Errore o Non valido in Corretto, selezionare il valore e quindi scegliere **Imposta i valori di dominio selezionati come corretti** (segno di spunta) dalla freccia giù nella barra delle icone o dall'elenco a discesa Tipo. Se il valore in errore o non valido viene raggruppato con un valore corretto, eliminare il valore dopo l'operazione.  
  
    -   **Imposta i valori di dominio selezionati come errori**: per modificare lo stato di un valore da Corretto o Non valido in Errore, selezionare il valore, quindi scegliere **Imposta i valori di dominio selezionati come errori** (segno di spunta) dalla freccia giù nella barra delle icone o dall'elenco a discesa Tipo. È possibile immettere una correzione nella colonna **Correggi in** o lasciarla vuota.  
  
    -   **Imposta i valori di dominio selezionati come non validi**: per modificare lo stato di un valore da Corretto o Errore in Non valido, selezionare il valore, quindi fare clic sull'icona **Imposta i valori di dominio selezionati come non validi** (triangolo) dalla freccia a discesa nella barra delle icone o dall'elenco a discesa Tipo. È possibile immettere una correzione nella colonna **Correggi in** o lasciarla vuota.  
  
    -   **Correggi in**: dopo avere impostato un valore come errore o non valido, immettere un nuovo valore nella colonna **Correggi in**. In DQS verrà aggiunta una nuova riga per il valore sostitutivo che verrà designato come valore corretto, quindi verranno raggruppati i due valori. Il nuovo valore verrà visualizzato come valore iniziale, con il valore iniziale in grassetto e il valore in errore o non valido rientrato.  
  
6.  Per designare i valori come gruppo di sinonimi, selezionare più valori corretti, quindi procedere come segue:  
  
    -   **Imposta i valori di dominio selezionati come sinonimi**: per impostare i sinonimi, selezionare più valori corretti, quindi fare clic sull'icona **Imposta i valori di dominio selezionati come sinonimi**. I valori verranno raggruppati e uno dei valori verrà definito come valore iniziale con cui verranno sostituiti gli altri valori. Si noti che se vengono raggruppati due valori, ma uno dei due valori del gruppo è in errore o non valido, i valori non saranno sinonimi.  
  
        > [!NOTE]  
        >  Se si selezionano due o più valori in un gruppo e un altro valore all'esterno del gruppo e quindi si impostano come sinonimi, verrà generato un messaggio di errore non corretto. Dopo avere chiuso la finestra popup del messaggio di errore, i valori verranno impostati correttamente come sinonimi.  
  
    -   **Interrompi relazione tra sinonimi selezionati**: per annullare la designazione di sinonimo per due o più valori, selezionare i valori, quindi fare clic sull'icona **Interrompi relazione tra sinonimi selezionati**. È necessario che i valori siano raggruppati ed entrambi devono essere corretti affinché l'annullamento del raggruppamento dei sinonimi venga eseguito correttamente.  
  
    -   **Imposta il valore di dominio selezionato come valore iniziale del gruppo**: per modificare il valore iniziale del gruppo, selezionare un valore nel gruppo non designato come valore iniziale, quindi fare clic sul pulsante **Imposta il valore di dominio selezionato come valore iniziale del gruppo**. In questo modo il valore iniziale verrà impostato come sostituzione dell'altro valore. Questa operazione funziona solo se sono stati impostati due o più valori raggruppati e si desidera modificare il valore iniziale rispetto al valore designato da DQS. Si noti che il valore iniziale viene indicato da una riga blu con il valore in grassetto.  
  
7.  **Correttore ortografico**: se un valore ha una sottolineatura rossa ondulata, il Correttore ortografico sta suggerendo una correzione del valore. Fare clic con il pulsante destro del mouse sul valore con la sottolineatura e selezionare una correzione, se appropriata. Il tipo di valore diventa (o rimane) in errore e la correzione verrà aggiunta alla colonna **Correggi in** . Fare clic sulla freccia in giù per visualizzare ulteriori correzioni proposte. Immettere una correzione manualmente per aggiungerla al dizionario del Correttore ortografico e poterla selezionare come correzione. Per ulteriori informazioni, vedere [Use the DQS Speller](../../2014/data-quality-services/use-the-dqs-speller.md) e [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Per utilizzare il Correttore ortografico, è possibile abilitarlo nella pagina **Proprietà dominio** o, se è disabilitato nella pagina **Proprietà dominio** , è possibile fare clic sull'icona **Abilita/Disabilita correttore ortografico** nella pagina **Valori di dominio** per abilitarlo in tale pagina.  
  
8.  **Aggiungi nuovo valore di dominio**: fare clic su questa opzione per aggiungere una riga alla fine della tabella. Dopo avere immesso un valore, la riga verrà riposizionata in ordine alfabetico preceduta da un asterisco per indicare che si tratta di una voce nuova.  
  
9. **Import domain values from Excel** (Importa valori di dominio da Excel): per aggiungere nuovi valori da un foglio di calcolo di Excel, fare clic sulla freccia a discesa corrispondente all'icona **Importa valori**, quindi selezionare **Import domain values from Excel** (Importa valori di dominio da Excel). Immettere il nome file, selezionare **Utilizza la prima riga come intestazione** se appropriato, quindi fare clic su **OK**. Per altre informazioni, vedere [Importare i valori da un file di Excel in un dominio](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
10. **Importa valori progetto**: per aggiungere nuovi valori da un progetto Data Quality, fare clic sulla freccia a discesa corrispondente all'icona **Importa valori**, quindi selezionare **Importa valori progetto**. Immettere il nome file, selezionare **Utilizza la prima riga come intestazione** se appropriato, quindi fare clic su **OK**. Selezionare il progetto da cui si desidera importare i valori, quindi fare clic su **OK**. Verranno visualizzati i valori importati. Scegliere **Fine**. Per ulteriori informazioni, vedere Importare i valori di progetto in un dominio.  
  
11. **Elimina valori di dominio selezionati**: per rimuovere uno o più valori esistenti dal dominio, selezionare i valori nella tabella dei valori, quindi fare clic sull'icona **Elimina valori di dominio selezionati**. Non è possibile eliminare il valore DQS_NULL, pertanto se si scelgono più valori da eliminare e il valore DQS_NULL è tra questi, l'operazione non riuscirà.  
  
12. Fare clic su **Fine** per completare l'attività di gestione del dominio, come descritto in [Sospensione dell'attività di gestione del dominio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="FollowUp"></a> Completamento: fasi successive alla modifica dei valori di dominio  
 Dopo avere modificato i valori di dominio, è possibile eseguire ulteriori attività di gestione del dominio, quali l'individuazione delle informazioni per aggiungere informazioni al dominio o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Meaning"></a> Significato dei valori Corretti, Errori e Non validi  
 A ogni valore nella tabella **Valore** della pagina **Valori di dominio** è assegnata un'impostazione **Tipo** di **Corretti**, **Errori**o **Non validi**. Il tipo del valore viene generato inizialmente dall'attività di individuazione delle informazioni ma è possibile modificarlo nel modo desiderato. Il tipo finale, basato sia sulle modifiche di individuazione che su quelle interattive, viene generato dall'attività di pulizia. Le impostazioni hanno il significato seguente:  
  
-   **Corretto:** si tratta di un valore che appartiene al dominio e non contiene errori di sintassi. Ad esempio, "Chicago" in un dominio Città è corretto.  
  
-   **Errore:** si tratta di un valore che appartiene al dominio, ma non è corretto. Ad esempio, "Shicago" anziché "Chicago" in un dominio Città è un errore. In DQS un valore viene definito come in errore quando nel processo di individuazione vengono rilevati un errore di sintassi e una correzione associata. Gli errori di sintassi includono gli errori di ortografia.  
  
-   **Non valido:** si tratta di un valore che non appartiene al dominio e a cui non è associata una correzione. Ad esempio, il valore "12345" in un dominio Città non è valido. In DQS un valore viene definito come non valido quando non supera una regola di dominio.  
  
 È possibile modificare manualmente l'impostazione Tipo scegliendo uno degli altri due valori. In DQS non viene applica la semantica della validità e dell'errore nelle operazioni manuali. È possibile immettere una correzione per un valore Non validi senza modificarne lo stato. È possibile definire un valore come non valido anche se ha superato una regola di dominio. È possibile definire un valore come in errore anche se il processo di individuazione non ha rilevato un errore di sintassi. È inoltre possibile rimuovere una correzione a un valore Errori, contrassegnato come Corretti, senza modificarne lo stato.  
  
 Quando si esegue la pulizia interattiva dei dati nella pagina **Gestisci e visualizza risultati** dell'attività **Pulizia** , nella scheda **Non validi** della pagina **Gestisci e visualizza risultati** vengono inclusi sia i valori in errore che quelli non validi.  
  
##  <a name="Display"></a> How to Display the Appropriate Values  
 È possibile modificare la visualizzazione come segue:  
  
-   **Filtrare** i risultati desiderati nella tabella, in base al relativo stato, selezionando lo stato nell'elenco a discesa **Filtro** .  
  
-   **Trovare** i dati che si desidera controllare o modificare immettendo una o più lettere da cercare nella casella di testo **Trova** . Tali lettere verranno evidenziate in tutti i valori visualizzati.  
  
-   Fare clic su **Mostra solo nuovi** per limitare i valori visualizzati nella tabella solo ai valori individuati nella sessione corrente, non nelle sessioni precedenti.  
  
-   Fare clic sul pulsante **Espandi tutto** per visualizzare tutti i valori in qualsiasi gruppo di sinonimi quando lo stato corrente è compresso.  
  
-   Fare clic sul pulsante **Comprimi tutto** per nascondere tutto tranne il valore iniziale in qualsiasi gruppo di sinonimi quando lo stato corrente è espanso.  
  
-   Fare clic sul pulsante **Mostra/Nascondi il pannello della cronologia delle modifiche dei valori di dominio** per visualizzare un'anteprima popup nella parte inferiore della tabella dei valori in cui vengono mostrate le modifiche recenti alla raccolta dei valori di dominio.  
  
##  <a name="Null"></a> Modalità di gestione degli equivalenti di un valore Null  
 Ogni tabella di valori nella scheda **Valori di dominio** include un valore DQS_NULL. Un valore Null in un'origine dati verrà visualizzato come valore SQL_NULL nella tabella di valori. È possibile impostare uno o più equivalenti di un valore Null come sinonimo di DQS_NULL. In tal modo, tutti i valori Null e gli equivalenti dei valori Null vengono elaborati come valori DQS_NULL.  
  
  
