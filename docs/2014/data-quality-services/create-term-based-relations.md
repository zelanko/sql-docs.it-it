---
title: Creare relazioni basate su termini | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.kbtermsbased.f1
ms.assetid: 66db9277-d892-4dae-8a82-060fd3ba6949
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54a899036513854d8a091165646b6fb4a955c962
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480823"
---
# <a name="create-term-based-relations"></a>Creare relazioni basate su termini
  In questo argomento viene descritto come creare relazioni basate su termini per un dominio in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Una relazione basata su termini (TRB) consente di effettuare una correzione a un termine che fa parte di un valore in un dominio, consentendo in questo modo a più valori identici ad eccezione dell'ortografia di una parte in comune tra essi di essere considerati sinonimi identici. È possibile, ad esempio, configurare una relazione basata su termini che modifica il termine "Inc." in "Incorporated". Il termine "Inc." verrà modificato ogni volta che viene trovato nel dominio. Le istanze di "Contoso, Inc." verranno modificate in "Contoso, Incorporated" e i due valori saranno considerati sinonimi esatti.  
  
 Per usare le relazioni basate su termini, è possibile compilare un elenco di coppie Valore/Correggi in, ad esempio "Inc." e "Incorporated" oppure "Senior" e "Sr.". L'utilizzo di una relazione basata su termini consente di modificare un termine in tutto il dominio senza impostare manualmente i valori di singoli domini come sinonimi. È possibile specificare di correggere un valore anche se l'individuazione delle informazioni non ha individuato tale valore in precedenza. Se una trasformazione delle relazioni basate su termini fa in modo che due valori siano identici, in DQS verrà creata tra essi una relazione di sinonimi (in individuazione delle informazioni), una relazione di correzioni (in correzione dei dati), o una corrispondenza esatta (in corrispondenza).  
  
 La trasformazione delle relazioni basate su termini e la trasformazione dei simboli (in cui i caratteri speciali vengono sostituiti da uno spazio o un valore Null) vengono entrambe eseguite in una fase di pre-elaborazione prima dell'analisi. Se è richiesta l'analisi di un dominio composito, essa verrà eseguita prima delle due trasformazioni, perché l'analisi basata su delimitatore richiede l'utilizzo di simboli. Altre operazioni, quali le regole di dominio e le modifiche ai valori del dominio, verranno eseguite dopo le trasformazioni. Per la corrispondenza, le relazioni basate su termini vengono applicate ai dati di origine prima dell'attività di individuazione delle corrispondenze indipendentemente dall'esecuzione della pulizia.  
  
 **Relazioni basate su termini e gestione del dominio**  
  
 Quando si applica una relazione basata su termini nella gestione dominio, le modifiche verranno applicate da DQS nell'individuazione delle informazioni, nella pulizia o nei processi di individuazione delle corrispondenze; tuttavia, il valore del dominio stesso non viene modificato da DQS per la conformità con la relazione basata su termini. In altre parole, se si inserisce e si accetta una relazione basata su termini nella scheda **Relazioni basate su termini** della pagina **Gestione dominio** , la modifica non verrà apportata nella scheda **Valori di dominio** della stessa pagina. Questo consente di modificare la TBR di conseguenza.  
  
 **Relazioni basate su termini e pulizia dei dati**  
  
 Quando si applica una relazione basata su termini in un dominio e si esegue il processo di pulizia dei dati, le modifiche vengono applicate da DQS durante la pulizia ma non ai termini nella knowledge base.  
  
-   Se un valore come è stato modificato da una relazione basata su termini si trova nel dominio, ma non si tratta di un sinonimo, verrà visualizzato nella colonna **Correggi in** nella scheda **Con correzione** della pagina **Gestisci e visualizza risultati** , con l'opzione Motivo impostata su Relazione basata su termini.  
  
-   Se un valore come è stato modificato da una relazione basata su termini non si trova nel dominio, e un valore corrispondente viene rilevato da DQS, il valore viene corretto e visualizzato nella scheda Con correzione o Suggeriti, in base al livello di confidenza. Se non viene trovata alcuna corrispondenza, il valore verrà visualizzato in Nuovi con una correzione TBR. Questa situazione si verifica perché anche se si corregge la TBR, non significa che il valore sia corretto.  
  
-   Se un valore come è stato modificato da una relazione basata su termini si trova nel dominio, ma il valore è Errori/Non validi con correzione esistente, verrà visualizzato nella scheda Con correzione insieme alla correzione e al valore di dominio motivo.  
  
-   Se un valore come è stato modificato da una relazione basata su termini si trova nel dominio, ma il valore è Errori/Non validi senza correzione, verrà visualizzato nella scheda Con correzione insieme alla correzione e al valore di dominio motivo.  
  
 **Relazioni basate su termini e individuazione delle informazioni**  
  
 Quando si applica una relazione basata su termini e si esegue il processo di individuazione delle informazioni, gli eventuali valori conformi alla TBR non vengono modificati e verranno identificati come un valore corretto. Qualsiasi valore modificato da una TBR verrà importato come valore corretto e identificato come un sinonimo di un valore conforme alla TBR.  
  
 **Relazioni basate su termini e importazione dei valori di pulizia in un dominio**  
  
 Se si importano informazioni sulla qualità dei dati raccolta durante il processo di pulizia in un dominio, un valore che è stato modificato da una TBR verrà importato come un valore corretto.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per creare relazioni basate su termini, è necessario disporre di un dominio aperto nell'attività Gestione dominio.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per creare relazioni basate su termini, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Create"></a>Creare relazioni basate su termini  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire o creare una Knowledge Base. Selezionare **Gestione dominio** come attività, quindi fare clic su **Apri** o **Crea**. Per ulteriori informazioni, vedere [Creare una Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md) o [Apertura di una Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La gestione del dominio viene eseguita in una pagina del client Data Quality Services che contiene cinque schede per le operazioni di gestione del dominio separate. Non si tratta di un processo basato su procedure guidate. Ciascuna operazione di gestione può essere eseguita separatamente.  
  
3.  Dall'**elenco di domini** nella pagina **Gestione dominio** selezionare il dominio per il quale si desidera creare una regola di dominio o creare un nuovo dominio. Se è necessario creare un nuovo dominio, vedere [Crea un dominio](../../2014/data-quality-services/create-a-domain.md).  
  
4.  Fare clic sulla scheda **Relazioni basate su termini** .  
  
5.  Creare le relazioni basate su termini come segue:  
  
    1.  Fare clic su **Aggiungi nuova relazione** per aggiungere una riga alla tabella Relazioni.  
  
    2.  Alla colonna **Valore** della riga aggiunta, immettere un termine che si desidera modificare ogni volta che si verifica in un valore nel dominio selezionato.  
  
        > [!NOTE]  
        >  Verrà visualizzato un errore se il termine esiste come valore intero nel dominio o se esiste già come valore in correzione nel dominio.  
  
    3.  Nella colonna **Correggi in** immettere un termine con cui si desidera modificare il termine nella colonna **Valore** .  
  
    4.  Fare di nuovo clic su **Aggiungi nuove relazioni** per aggiungere un'altra relazione basata su termini.  
  
    5.  Fare clic su **Elimina relazioni selezionate** per eliminare una o più righe selezionate dalla tabella Relazioni. Per selezionare più righe, fare clic su una riga non selezionata tenendo premuto il pulsante CTRL.  
  
    6.  Trovare un valore nella tabella Relazioni immettendo una o più cifre nella casella di testo **Trova** . Le corrispondenze per la stringa verranno evidenziate. Utilizzare le frecce in su o in giù per spostarsi tra le diverse istanze della stringa nella tabella.  
  
    7.  **Correttore ortografico**: se un valore nella colonna **valore** o **Correggi a** ha una sottolineatura rossa ondulata, il correttore ortografico sta suggerendo una correzione per il valore. Fare clic con il pulsante destro del mouse sul valore con il carattere di sottolineatura e selezionare uno dei valori proposti dal correttore ortografico. In alternativa, è possibile fare clic su **Aggiungi** nel menu di scelta rapida per mantenere il valore originale. Per ulteriori informazioni, vedere [Utilizzare il correttore ortografico DQS](../../2014/data-quality-services/use-the-dqs-speller.md) e [Imposta proprietà del dominio](../../2014/data-quality-services/set-domain-properties.md).  
  
        > [!NOTE]  
        >  Per utilizzare il correttore ortografico, è possibile abilitarlo nella pagina **Proprietà dominio** o, se è disabilitato nella pagina **Proprietà dominio** , è possibile fare clic sull'icona **Abilita/Disabilita correttore ortografico** nella pagina **Relazioni basate su termini** per abilitarlo in tale pagina.  
  
6.  Fare clic su **Applica modifiche** per applicare le relazioni basate su termini al dominio.  
  
7.  Fare clic su **Fine** per completare l'attività di gestione del dominio, come descritto in [Sospensione dell'attività di gestione del dominio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="FollowUp"></a>Completamento: fasi successive alla creazione di relazioni basate su termini  
 Dopo avere creato le relazioni basate su termini, è possibile eseguire ulteriori attività di gestione del dominio, quali l'individuazione delle informazioni per aggiungere informazioni al dominio o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
