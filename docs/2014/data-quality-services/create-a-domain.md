---
title: Creare un dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54c1a720f34a7cce978371a6794f41e8af5f3b24
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480966"
---
# <a name="create-a-domain"></a>Creazione di un dominio
  In questo argomento viene descritto come creare un dominio in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). I valori nel dominio sono una rappresentazione semantica dei dati in un campo. Per altre informazioni sui domini, vedere [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md).  
  
 Sono disponibili due modi per creare un nuovo dominio. Il primo viene utilizzato durante il passaggio di mapping dell'attività di individuazione delle informazioni, quando è in corso l'analisi di un campione di dati per aggiungere informazioni a una Knowledge Base nuova o esistente. Il secondo viene utilizzato durante l'attività di gestione del dominio, quando anziché modificare un dominio esistente, se ne crea uno nuovo.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per creare un dominio, è necessario avere creato e aperto una Knowledge Base.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per creare un dominio, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="create-a-domain-in-the-knowledge-discovery-activity"></a><a name="Discovery"></a> Creare un dominio nell'attività di individuazione delle informazioni  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri Knowledge Base** , quindi selezionare una Knowledge Base o fare clic su **Nuova Knowledge Base** e immettere le proprietà per la nuova Knowledge Base.  
  
3.  Selezionare **Individuazione informazioni** come attività, quindi fare clic su **Crea** per creare la nuova Knowledge Base, oppure **Apri** per aprirne una esistente.  
  
4.  Nella pagina **Mappa** specificare una connessione all'origine dati. Per ulteriori informazioni, vedere [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md).  
  
5.  Nella tabella **Mapping** selezionare una colonna di origine dall'elenco a discesa per la **Colonna di origine** di una riga vuota. Se non esiste alcun dominio corrispondente, fare clic sull'icona **Crea un dominio** .  
  
##  <a name="create-a-domain-in-the-domain-management-activity"></a><a name="DomainManagement"></a>Creare un dominio nell'attività di gestione del dominio  
  
1.  Nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri Knowledge Base** , quindi selezionare una Knowledge Base o fare clic su **Nuova Knowledge Base** e immettere le proprietà per la nuova Knowledge Base.  
  
2.  Selezionare **Gestione dominio** come attività, quindi fare clic su **Crea** per creare la nuova Knowledge Base, oppure **Apri** per aprirne una esistente.  
  
3.  Nella pagina **Gestione dominio** fare clic sull'icona **Crea un dominio** sopra l'elenco di domini.  
  
##  <a name="set-domain-properties"></a><a name="Properties"></a>Impostare le proprietà del dominio  
  
1.  Nella finestra di dialogo **Crea dominio** immettere un nome univoco per la Knowledge Base e una descrizione di un massimo di 256 caratteri.  
  
    > [!NOTE]  
    >  Per ulteriori informazioni sulle proprietà del dominio, vedere [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md).  
  
2.  Dall'elenco **Tipo di dati** selezionare un tipo di dati per i valori nel dominio. Il tipo di dati può essere **Stringa** (valore predefinito), **Data**, **Intero**o **Decimale**.  
  
3.  Selezionare **Utilizza valori iniziali** per specificare che venga restituito il valore iniziale in un gruppo di sinonimi anziché un valore di cui è sinonimo. Deselezionare **Utilizza valori iniziali** per specificare che ogni valore di sinonimo verrà restituito nella forma corretta e non verrà sostituito dal valore iniziale per il gruppo.  
  
4.  Se il tipo di dati è **Stringa**, selezionare **Normalizza stringa** per rimuovere i caratteri speciali nei valori di dominio migliorando la probabilità di corrispondenze.  
  
5.  Dall'elenco a discesa **Formato output in** selezionare la formattazione che verrà applicata alla restituzione dei valori dei dati nel dominio. La formattazione è specifica del tipo di dati selezionato nel passaggio 2, come mostrato nell'elenco seguente:  
  
    -   Per un valore stringa, è possibile specificare di restituire la stringa tutta in maiuscole, tutta in minuscole o solo con l'iniziale maiuscola.  
  
    -   Per un valore data, è possibile specificare il formato del giorno, del mese e dell'anno.  
  
    -   Per un valore intero, è possibile specificare il tipo di maschera del formato da applicare.  
  
    -   Per un valore decimale, è possibile specificare la precisione e il tipo di maschera del formato da applicare.  
  
     Se si seleziona **Nessuno** nell'elenco a discesa **Formato output in** non verrà applicato alcun formato tra quelli elencati.  
  
6.  Se il tipo di dati è **Stringa**, nell'elenco a discesa **Lingua** selezionare la lingua da utilizzare per il correttore ortografico se viene abilitato.  
  
7.  Se il tipo di dati è **Stringa**, selezionare **Abilita correttore ortografico** per eseguire il correttore ortografico su tutti i valori stringa durante l'inserimento nel dominio.  
  
8.  Se il tipo di dati è **Stringa**, selezionare **Disabilita algoritmi di errore sintassi** per popolare il dominio senza verificare la presenza di errori di sintassi nei valori stringa.  
  
9. Fare clic su **OK**.  
  
10. Fare clic su **Fine** per completare l'attività di gestione del dominio, come descritto in [Sospensione dell'attività di gestione del dominio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="follow-up-after-creating-a-domain"></a><a name="FollowUp"></a> Completamento: fasi successive alla creazione di un dominio  
 Dopo avere creato un dominio, è possibile eseguire ulteriori attività di gestione del dominio, quali l'individuazione delle informazioni per aggiungere informazioni al dominio o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
