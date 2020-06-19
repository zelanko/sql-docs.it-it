---
title: Creare una regola tra domini | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.testcdrule.f1
- sql12.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 607bab94349fc2d32362647dc44ab27b84690f5f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937942"
---
# <a name="create-a-cross-domain-rule"></a>Creare una regola tra domini
  In questo argomento viene descritto come creare una regola tra domini per un dominio composito in una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Una regola tra domini consente di testare la relazione tra i valori nei singoli domini inclusi in un dominio composito. Una regola tra domini deve rimanere valida in tutto un dominio composito affinché i valori di dominio vengano considerati accurati e conformi ai requisiti aziendali. Una regola tra domini viene utilizzata per convalidare, correggere e standardizzare i valori di dominio.  
  
 Le clausole If e Then di una regola tra domini sono definite ognuna per uno dei singoli domini del dominio composito. Ogni clausola deve essere definita per un singolo dominio diverso. Una regola tra domini deve essere correlata a più singoli domini. Non è possibile definire una regola di dominio semplice (solo per un singolo dominio) per un dominio composito. Questa operazione viene effettuata definendo una regola di dominio per un singolo dominio. Le clausole If e Then possono contenere ognuna una o più condizioni.  
  
 Una regola tra domini con condizioni definitive applicherà la logica delle regole ai sinonimi del valore nelle condizioni, oltre ai valori stessi. Le condizioni definitive per le clausole If e Then sono: Il valore è uguale a, Il valore è diverso da, Il valore è in o Il valore non è in. Si supponga ad esempio di disporre della regola tra domini seguente per un dominio composito: "Se per 'City' il valore è uguale a 'Los Angeles', per 'State' il valore è uguale a 'CA'". Se 'Los Angeles e 'LA' sono sinonimi, questa regola restituirà un risultato corretto per 'Los Angeles CA' e 'LA CA' ma un risultato in errore per 'Los Angeles WA' e 'LA WA'.  
  
 Oltre a indicare la validità di una regola tra domini, la clausola definitiva *Then* in una regola tra domini, **Il valore è uguale a**, corregge anche i dati durante l'attività di pulizia dei dati. Per ulteriori informazioni, vedere [Data Correction using Definitive Cross-Domain Rules](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) in [Cleanse Data in a Composite Domain](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md).  
  
 Le regole tra domini vengono prese in esame dopo tutte le regole semplici applicate solo a un singolo dominio. Solo se un valore supera le singole regole di dominio (se esistono) verrà applicata la regola tra domini. Il dominio composito e i singoli domini su cui viene eseguita una regola devono tutti essere definiti prima dell'esecuzione della regola.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per creare una regola tra domini, è necessario avere creato e aperto un dominio composito.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN per creare una regola tra domini.  
  
##  <a name="create-cross-domain-rules"></a><a name="Create"></a> Creare le regole tra domini  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire o creare una Knowledge Base. Selezionare **Gestione dominio** come attività, quindi fare clic su **Apri** o **Crea**. Per ulteriori informazioni, vedere [Creare una Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md) o [Apertura di una Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La gestione del dominio viene eseguita in una pagina del client Data Quality Services che contiene cinque schede per le operazioni di gestione del dominio separate. Non si tratta di un processo basato su procedure guidate. Ciascuna operazione di gestione può essere eseguita separatamente.  
  
3.  **Dall'elenco di domini** nella pagina **Gestione dominio** selezionare il dominio composito per il quale si desidera creare una regola di dominio o creare un nuovo dominio composito. Se è necessario creare un nuovo dominio, vedere [Create a Composite Domain](../../2014/data-quality-services/create-a-composite-domain.md).  
  
4.  Fare clic sulla scheda **Regole CD** .  
  
5.  Fare clic su **Aggiungi una nuova regola di domini**, quindi immettere un nome e una descrizione per la regola.  
  
6.  Selezionare **Attiva** per specificare che la regola verrà eseguita (valore predefinito) o deselezionare per impedire l'esecuzione della regola.  
  
7.  Creare la clausola If come segue:  
  
    1.  Nell'elenco di domini del riquadro della clausola If selezionare uno dei singoli domini inclusi nel dominio composito da includere come oggetto della clausola If. È possibile selezionare qualsiasi singolo dominio nel dominio composito.  
  
    2.  Selezionare una condizione dall'elenco a discesa per la prima condizione della clausola.  
  
    3.  Se la condizione richiede un valore, immettere il valore nella casella di testo associata.  
  
    4.  Se la clausola If richiede un'altra condizione, fare clic su **Aggiunge una nuova condizione alla clausola selezionata**. Selezionare l'operatore, selezionare una condizione e immettere un valore per la condizione, se necessario.  
  
    5.  Per modificare l'ordine delle condizioni, selezionare una condizione facendo clic a sinistra della condizione, quindi fare clic sulla freccia Su o Giù.  
  
    6.  Per nascondere le condizioni, fare clic sul segno meno a sinistra del nome del dominio. Per visualizzare le condizioni, fare clic sul segno più.  
  
8.  Creare la clausola Then selezionando un singolo dominio, diverso dall'oggetto della clausola If, nell'elenco di domini del riquadro della clausola Then. Compilare quindi la clausola Then utilizzando gli stessi passaggi effettuati per la compilazione della clausola If.  
  
9. Continuare con la procedura relativa al test descritta di seguito.  
  
##  <a name="test-cross-domain-rules"></a><a name="Test"></a> Testare le regole tra domini  
  
1.  Testare la regola tra domini come segue:  
  
    1.  Fare clic sull'icona **Esegui la regola del dominio selezionato sui dati di test** nell'angolo in alto a destra del riquadro del dominio composito.  
  
    2.  Nella finestra di dialogo **Esegui la regola di dominio** fare clic sull'icona **Aggiunge un nuovo termine di test per la regola di dominio** .  
  
    3.  Immettere i valori di test per il singolo dominio associato alla clausola If e per il singolo dominio associato alla clausola Then. I valori di test immessi nella clausola If devono soddisfare le condizioni per tale clausola, altrimenti verrà immesso un punto interrogativo nella colonna **Validità** a indicare che la regola tra domini non è valida per i dati di test.  
  
    4.  Fare di nuovo clic sull'icona **Aggiunge un nuovo termine di test per la regola di dominio** per aggiungere un altro set di valori di test.  
  
    5.  Fare clic sull'icona **testa la regola di dominio su tutti i termini** . Se un set di valori di test è valido, nella colonna **Validità** verrà immesso un segno di spunta per la riga. Se il set di valori di test non è valido, nella colonna Validità verrà immesso un triangolo con un punto esclamativo per la riga.  
  
    6.  Al termine del test fare clic su **Chiudi** nella finestra di dialogo **Test regola dominio composito** .  
  
2.  Dopo aver completato le regole tra domini, fare clic su **Fine** per completare l'attività di gestione del dominio, come descritto in [End the Domain Management Activity](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="follow-up-after-creating-a-cross-domain-rule"></a><a name="FollowUp"></a> Completamento: fasi successive alla creazione di una regola tra domini  
 Dopo avere creato una regola tra domini, è possibile eseguire ulteriori attività di gestione del dominio, quali l'individuazione delle informazioni per aggiungere informazioni al dominio o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
