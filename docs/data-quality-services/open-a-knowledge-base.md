---
title: Apertura di una Knowledge Base
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.openkb.f1
ms.assetid: a5f010a5-b762-41c9-881b-bf0c192dca83
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 91f5e7effe54b9955537d90d639a820b5428a5c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246014"
---
# <a name="open-a-knowledge-base"></a>Apertura di una Knowledge Base

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come aprire una Knowledge Base esistente in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) e prepararla per le attività di gestione del dominio, individuazione delle informazioni o aggiunta di criteri di corrispondenza.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per aprire una Knowledge Base, è necessario che questa sia già stata creata e pubblicata (se creata da un altro utente) o chiusa (se creata dallo stesso utente).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per aprire una Knowledge Base è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Open"></a>Aprire una Knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Apri Knowledge Base**.  
  
3.  Selezionare una Knowledge Base nella tabella. I domini e le regole di corrispondenza nella Knowledge Base verranno visualizzati nel riquadro nella parte destra della pagina.  
  
    > [!NOTE]  
    >  È possibile eseguire operazioni su una Knowledge Base facendo clic con il pulsante destro del mouse su di essa nella tabella. È possibile aprire la Knowledge Base, salvarla con un nome diverso, sbloccarla, annullare le modifiche apportatevi, rinominarla o visualizzarne le proprietà.  
  
4.  In **Seleziona attività**, selezionare l'attività che si desidera eseguire sulla Knowledge Base:  
  
    -   Selezionare **Gestione dominio** per accedere alle schermate per la modifica dei domini nella Knowledge Base.  
  
    -   Selezionare **Individuazione informazioni** per avviare la procedura guidata che consente di analizzare un campione di dati e di popolare i domini della Knowledge Base con i risultati.  
  
    -   Selezionare **Criteri di corrispondenza** per creare criteri di corrispondenza e aggiungerli alla Knowledge Base.  
  
5.  Fare clic su **Apri**.  
  
    > [!NOTE]  
    >  È inoltre possibile aprire la Knowledge Base facendo clic con il pulsante destro del mouse su di essa e quindi scegliendo Apri. Altri comandi disponibili nel menu di scelta rapida consentono di salvare la Knowledge Base con un nome diverso, sbloccarla, annullare le modifiche apportatevi, rinominarla o visualizzarne le proprietà.  
  
    > [!NOTE]  
    >  Se non è possibile aprire la Knowledge Base perché bloccata, vedere la sezione seguente.  
  
## <a name="open-a-recent-knowledge-base"></a>Apertura di una Knowledge Base recente  
 Le cinque Knowledge Base aperte più recentemente sono visualizzate nell'elenco **Knowledge Base recente** nella home page di DQS. Ciò consente di aprire una Knowledge Base con cui si è lavorato recentemente senza passare per la pagina **Apri Knowledge Base** .  
  
-   Per aprire una Knowledge Base non bloccata e presente nell'elenco delle Knowledge Base recenti, fare clic sulla freccia destra relativa alla Knowledge Base desiderata, quindi selezionare l'attività nella quale avviare la Knowledge Base.  
  
-   Per aprire una Knowledge Base presente nell'elenco delle Knowledge Base recenti ma che è stata bloccata dall'utente che vi sta lavorando, fare clic sulla Knowledge Base e la Knowledge Base verrà aperta nell'attività e nella pagina indicate tra parentesi.  
  
-   Per aprire una Knowledge Base presente nell'elenco delle Knowledge Base recenti ma che è stata bloccata da un altro utente, contattare l'utente per richiederne lo sblocco.  
  
##  <a name="FollowUp"></a>Completamento: dopo l'apertura di una Knowledge base  
 Dopo avere aperto una Knowledge Base, questa viene collocata nello stato indicato nella colonna Stato della relativa tabella. Per le attività di individuazione delle informazioni e quelle relative ai criteri di corrispondenza, la Knowledge Base verrà aperta in una pagina di procedura guidata specifica. Per l'attività di gestione del dominio, la Knowledge Base verrà aperta nella pagina di gestione del dominio. Per altre informazioni sugli stati, vedere [Eseguire l'individuazione delle informazioni](../data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Locked"></a>Se la Knowledge base è bloccata  
 L'icona di blocco nella prima colonna indica se la Knowledge Base è bloccata. Il nome di una Knowledge Base bloccata verrà visualizzato in colore rosso. Una Knowledge Base in corso di modifica da parte di un utente specifico tramite un'attività di Knowledge Base, viene contrassegnata come Bloccata. Una Knowledge Base bloccata non può essere modificata da un secondo utente. L'utente che sta lavorando alla Knowledge Base può sbloccarla facendo clic su di essa con il pulsante destro del mouse nella tabella presente nella pagina Apri Knowledge Base, quindi scegliendo **Sblocca**, oppure può sbloccarla effettuandone la pubblicazione. Quando si posiziona il cursore su una Knowledge Base bloccata, viene visualizzato un suggerimento in DQS che indica chi ha bloccato la Knowledge Base e quando.  
  
##  <a name="State"></a>Stato di una Knowledge base  
 Nel campo Stato viene indicata la fase di un'attività a cui si trova la Knowledge Base. Se si apre la Knowledge Base, verrà aperta in quella fase.  
  
-   >vuota: il campo stato è vuoto per una Knowledge base se la Knowledge base è stata pubblicata facendo clic su **pubblica** nell'attività Gestione dominio e quindi su **Sì-pubblica la Knowledge base e Chiudi**. ** \< **  
  
-   **In lavorazione**: il lavoro sulla Knowledge base è stato salvato facendo clic su **pubblica** nell'attività Gestione dominio e quindi su **No-Salva il lavoro sulla Knowledge base e Chiudi**.  
  
-   **Gestione dominio**: sono stati immessi dati per un dominio nella Knowledge base, ma la Knowledge base non è stata pubblicata e il lavoro rimane nell'attività di gestione del dominio. L'attività Individuazione informazioni non è disponibile. Ciò si verifica quando si fa clic su **Chiudi** nella schermata **Gestione dominio** .  
  
-   **Individuazione-mapping**: la Knowledge base è stata chiusa nella pagina **Gestione Knowledge Base: mapping** . La Knowledge Base è bloccata e le attività di gestione del dominio e di individuazione delle corrispondenze non sono disponibili.  
  
-   **Individuazione-** individuazione: la Knowledge base è stata chiusa nella pagina **Gestione Knowledge Base: analizza** . La Knowledge Base è bloccata e l'attività di gestione del dominio non è disponibile.  
  
-   **Gestione dei valori di individuazione**: la Knowledge base è stata chiusa nella pagina **Gestione Knowledge Base: Gestisci termini di dominio** . La Knowledge Base è bloccata e l'attività di gestione del dominio non è disponibile.  
  
-   Criteri di corrispondenza **-criteri di corrispondenza**: la Knowledge base è stata chiusa nella pagina **criteri di corrispondenza-criteri di** corrispondenza. La Knowledge Base è bloccata e le attività di gestione del dominio e di individuazione delle informazioni non sono disponibili.  
  
-   **Criteri di corrispondenza-risultati corrispondenza**: la Knowledge base è stata chiusa nella pagina **criteri di corrispondenza-risultati corrispondenza** . La Knowledge Base è bloccata e le attività di gestione del dominio e di individuazione delle informazioni non sono disponibili.  
  
  
