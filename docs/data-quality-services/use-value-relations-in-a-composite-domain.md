---
title: Utilizzare le relazioni di valori in un dominio composito
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 90937a98bb409c6f17bc542183cd024f408d71f2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257758"
---
# <a name="use-value-relations-in-a-composite-domain"></a>Utilizzare le relazioni di valori in un dominio composito

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come visualizzare le combinazioni di valori presenti nel dominio composito durante il processo di individuazione delle informazioni in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). In questa pagina viene illustrato il numero di occorrenze delle combinazioni di valori. La gestione dei valori non è supportata per i domini compositi, pertanto non è possibile eseguire alcuna operazione su questi valori.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per visualizzare le relazioni di valori, è necessario avere creato e aperto un dominio composito.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per visualizzare le relazioni di valori in un dominio composito, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="view-value-relations"></a><a name="Use"></a>Visualizza relazioni tra valori  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire o creare una Knowledge Base. Selezionare **Gestione dominio** come attività, quindi fare clic su **Apri** o **Crea**. Per ulteriori informazioni, vedere [Creare una Knowledge Base](../data-quality-services/create-a-knowledge-base.md) o [Apertura di una Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
3.  **Dall'elenco di domini** nella pagina **Gestione dominio** selezionare il dominio composito per il quale si desidera creare una regola di dominio o creare un nuovo dominio composito. Se è necessario creare un nuovo dominio, vedere [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
4.  Fare clic sulla scheda **Relazioni valore** .  
  
5.  Visualizzare le frequenze riportate per ogni combinazione di valori.  
  
    > [!NOTE]  
    >  Nella tabella **Valore** viene visualizzata ogni combinazione di valori presente nel dominio composito. Ogni valore viene mostrato nel singolo dominio a cui si applica. L'ordinamento predefinito della tabella delle relazioni di valori è per frequenza, ma è possibile fare clic su un'altra colonna per ordinare in base a tale colonna. Vengono visualizzati solo i valori con una frequenza maggiore o uguale a 20.  
  
6.  Non è possibile modificare alcun valore nella tabella. Se sono state eseguite le altre operazioni, fare clic su **Fine** per completare l'attività di gestione del dominio. In caso contrario, fare clic su **Annulla**.  
  
##  <a name="follow-up-after-viewing-value-relations"></a><a name="FollowUp"></a>Completamento: fasi successive alla visualizzazione delle relazioni tra valori  
 Dopo avere visualizzato le relazioni di valori, è possibile eseguire ulteriori attività di gestione del dominio, quali l'individuazione delle informazioni per aggiungere informazioni al dominio o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md).  
  
  
