---
title: Gestire una Knowledge Base | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 552cd3a091699c42001ab42e64ff875760fe1e53
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484169"
---
# <a name="manage-a-knowledge-base"></a>Gestire una Knowledge Base
  In questo argomento viene descritto come eseguire le funzioni di gestione su una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). È possibile eliminare una Knowledge Base, sbloccarla, annullare le modifiche apportatevi, rinominarla e visualizzarne le proprietà.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per gestire una Knowledge Base, è necessario che questa sia già stata creata e pubblicata (se creata da un altro utente) o chiusa (se creata dallo stesso utente).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per aprire una Knowledge Base è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Manage"></a>Gestire una Knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Apri Knowledge Base**.  
  
3.  Fare clic con il pulsante destro del mouse su una Knowledge Base nella relativa tabella.  
  
4.  Nel menu di scelta rapida è possibile scegliere tra le opzioni seguenti:  
  
    1.  **Apri**: fare clic per aprire la Knowledge base nell'attività selezionata nel riquadro **Seleziona attività** .  
  
    2.  **Sblocca**: è possibile sbloccare la Knowledge base se si è l'utente che stava lavorando alla Knowledge base in uno dei passaggi di gestione del dominio, individuazione delle informazioni e attività dei criteri di corrispondenza e chiuso. Se si sblocca la Knowledge Base, un altro utente potrà aprirla e utilizzarla. Questo comando non è disponibile se la Knowledge Base non si trova in uno stato di un'attività. Per altre informazioni, vedere [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    3.  Annulla **lavoro**: fare clic quando la Knowledge base si trova in uno stato di lavorazione, come illustrato con una voce nel campo stato della tabella. Questo comando non è disponibile se la Knowledge Base non si trova in uno stato di un'attività e se la Knowledge Base è bloccata. Per altre informazioni, vedere [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    4.  **Rinomina**: fare clic per rendere modificabile il campo Knowledge base della tabella per la Knowledge base su cui si è fatto clic con il pulsante destro del mouse. Modificare il nome, quindi fare clic sulla Knowledge Base e nel campo per accettare la modifica del nome.  
  
    5.  **Elimina**: fare clic per rimuovere la Knowledge base dal database DQS_MAIN [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
    6.  **Proprietà**: fare clic per visualizzare le proprietà del database in una visualizzazione di sola lettura.  
  
        1.  **Knowledge base origine**: la Knowledge base su cui si basava il database. Operazione facoltativa.  
  
        2.  **Stato**: indica se la Knowledge base è **in lavorazione** e se si trova in un'attività di gestione delle informazioni specifica, come stabilito al momento dell'ultima chiusura. Lo stato può essere **In lavorazione**in cui la Knowledge Base viene aperta in una sessione di gestione delle informazioni, ma non in un'attività specifica, o **In lavorazione** con un'attività di gestione delle informazioni in cui la Knowledge Base viene aperta in una sessione di gestione delle informazioni e in un'attività specifica.  
  
        3.  **Bloccato**: **true** se la Knowledge base è bloccata, **false** in caso contrario.  
  
        4.  **Contiene contenuto non pubblicato**: true se la Knowledge base contiene contenuto non salvato tramite pubblicazione, false in caso contrario.  
  
        5.  **Bloccato da**: nome dell'utente che ha chiuso la Knowledge base, blocco  
  
        6.  **Data di blocco**: data di blocco  
  
        7.  **Creato da**: nome dell'utente che ha creato la Knowledge base, con la rete a cui appartiene  
  
        8.  **Data di creazione**: data di creazione  
  
##  <a name="FollowUp"></a>Completamento: fasi successive alla gestione di una Knowledge base  
 Dopo avere gestito una Knowledge Base, il passaggio successivo dipende dall'azione intrapresa sulla Knowledge Base:  
  
-   Se la Knowledge Base è stata aperta, l'utente continuerà nell'attività selezionata.  
  
-   Se è stata sbloccata, la Knowledge Base potrà essere aperta e utilizzata da un altro utente nello stato indicato.  
  
-   Se vi sono state annullate le modifiche apportate, la Knowledge Base sarà disponibile nell'ultimo stato pubblicato.  
  
-   Se è stata rinominata, sarà necessario aprire la Knowledge Base rinominata.  
  
-   Se è stata eliminata, sarà necessario selezionare un'altra Knowledge Base o crearne una nuova.  
  
  
