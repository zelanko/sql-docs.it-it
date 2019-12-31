---
title: Creare una Knowledge Base
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 20421ab3584eac51feb09ba717f293449825574c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247329"
---
# <a name="create-a-knowledge-base"></a>Creare una Knowledge Base

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come creare una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) e prepararla per le attività di gestione del dominio, individuazione delle informazioni o aggiunta di criteri di corrispondenza.  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
  
###  <a name="Prerequisites"></a>Prerequisiti  
 Per creare una Knowledge Base, è necessario avere installato il [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Per creare una Knowledge Base, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Createaknowledgebase"></a>Creare una Knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Nuova Knowledge Base**.  
  
3.  Immettere un nome e una descrizione per la nuova Knowledge Base.  
  
4.  In **Crea Knowledge Base da**selezionare l'elemento sui cui basare la Knowledge Base.  
  
    -   Selezionare **Nessuno** se non si desidera basare la nuova Knowledge Base su una Knowledge Base esistente o su un file di dati.  
  
    -   Selezionare **Knowledge Base esistente** per basare la nuova Knowledge Base su una Knowledge Base già creata nel [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]o sulla Knowledge Base predefinita. Selezionare la Knowledge Base dall'elenco a discesa **Seleziona Knowledge Base** o fare clic su **Sfoglia** per visualizzare la finestra di dialogo **Selezionare una Knowledge Base** , selezionare una Knowledge Base esistente su cui basare la nuova Knowledge Base, quindi fare clic su **OK**. Quando si seleziona una Knowledge Base dalla tabella, i domini e le regole di corrispondenza nella Knowledge Base verranno visualizzati nel riquadro a destra della finestra di dialogo. È anche possibile selezionare **Dati DQS** , la Knowledge Base predefinita che contiene i domini comuni predefiniti e le informazioni correlate a dati di società, indirizzi e soggetti negli Stati Uniti.  
  
    -   Selezionare **Importa da file DQS** per basare la nuova Knowledge Base su un file DQS nel [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Fare clic su **Sfoglia**, selezionare un file di dati DQS con un'estensione DQS, quindi fare clic su **OK**.  
  
5.  In **Seleziona attività**selezionare l'attività che si desidera eseguire sulla nuova Knowledge Base:  
  
    -   Selezionare **Gestione dominio** per creare la Knowledge Base e visualizzare le schermate per la modifica dei domini nella Knowledge Base.  
  
    -   Selezionare **Individuazione informazioni** per creare la Knowledge Base e avviare la procedura guidata che consente di analizzare un campione di dati e di popolare i domini della Knowledge Base con i risultati.  
  
    -   Selezionare **Criteri di corrispondenza** per creare criteri di corrispondenza e aggiungerli alla Knowledge Base.  
  
6.  Fare clic su **Crea**.  
  
##  <a name="FollowUp"></a>Completamento: fasi successive alla creazione di una Knowledge base  
 Dopo avere creato una Knowledge Base, vengono visualizzate una procedura guidata che consente di eseguire l'individuazione delle informazioni, una procedura guidata per creare i criteri di corrispondenza o le pagine per eseguire la gestione del dominio. Per altre informazioni sull'individuazione delle informazioni, sulla gestione del dominio o sui criteri di corrispondenza, vedere [Eseguire l'individuazione di informazioni](../data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../data-quality-services/managing-a-domain.md), o [Creare criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md).  
  
  
