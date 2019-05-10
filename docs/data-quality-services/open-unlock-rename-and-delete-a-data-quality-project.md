---
title: Aprire, sbloccare, rinominare ed eliminare un progetto Data Quality | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fc7dc1a8ca0aac433d10c22770c70f18d44c8f3e
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488260"
---
# <a name="open-unlock-rename-and-delete-a-data-quality-project"></a>Aprire, sbloccare, rinominare ed eliminare un progetto Data Quality

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come gestire un progetto Data Quality utilizzando [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ed effettuare operazioni sul progetto quali apertura, ridenominazione ed eliminazione.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile aprire un progetto bloccato creato da un altro utente.  
  
-   Non è possibile sbloccare, rinominare o eliminare progetti Data Quality creati da altri utenti.  
  
-   Non è possibile eliminare un progetto Data Quality bloccato. È necessario procedere allo sblocco prima dell'eliminazione.  
  
-   È possibile sbloccare solo progetti Data Quality creati dall'utente che sta procedendo allo sblocco.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario avere almeno un progetto Data Quality da gestire.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per gestire un progetto Data Quality è necessario disporre del ruolo dqs_kb_editor o dqs_kb_operator nel database DQS_MAIN.  
  
##  <a name="Open"></a> Apertura di un progetto Data Quality  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
     Alternativamente, è possibile aprire direttamente un progetto Data Quality elencato nell'area **Progetto Data Quality recente** facendo clic su di esso.  
  
3.  Nella finestra di dialogo **Apri progetto** fare clic per selezionare il progetto Data Quality che si desidera aprire, quindi fare clic su **Avanti**.  
  
4.  Il progetto Data Quality viene aperto nello stesso stato in cui era stata chiusa l'ultima volta l'attività. Un progetto Data Quality può presentare gli stati seguenti:  
  
    -   Per l'attività **Pulizia**, un progetto Data Quality può presentare gli stati seguenti: **Pulizia - Mappa**, **Pulizia - Pulisci**, **Pulizia - Gestisci e visualizza risultati** e **Pulizia - Esportazione**.  
  
    -   Per l'attività **Corrispondenza**, un progetto Data Quality può presentare gli stati seguenti: **Corrispondenza - Mappa**, **Corrispondenza - Corrispondenza**, **Corrispondenza - Sopravvivenza** e **Corrispondenza - Esportazione**.  
  
##  <a name="Unlock"></a> Sblocco di un progetto Data Quality  
 Quando viene creato, un progetto Data Quality è impostato in uno stato bloccato per impedire l'utilizzo o la modifica da parte di altri utenti. Se si desidera che altri utenti possano lavorare sul progetto Data Quality, una volta completate le proprie attività è necessario sbloccare il progetto. Per i progetti bloccati, viene visualizzato un simbolo a forma di lucchetto.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella schermata **Apri progetto** , fare clic con il pulsante destro del mouse su un progetto Data Quality bloccato che sia stato creato dall'utente corrente, quindi scegliere **Sblocca** dal menu di scelta rapida. Viene visualizzato un segno di spunta verde che indica che il progetto è ora sbloccato.  
  
##  <a name="Rename"></a> Ridenominazione di un progetto Data Quality  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella schermata **Apri progetto** , fare clic con il pulsante destro del mouse su un progetto Data Quality bloccato che sia stato creato dall'utente corrente, quindi scegliere **Rinomina** dal menu di scelta rapida.  
  
4.  Il nome del progetto Data Quality diventa modificabile nella colonna **Nome** . Digitare un nuovo nome e premere INVIO.  
  
##  <a name="Delete"></a> Eliminazione di un progetto Data Quality  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella schermata **Apri progetto** , fare clic con il pulsante destro del mouse su un progetto Data Quality sbloccato che sia stato creato dall'utente corrente, quindi scegliere **Elimina** dal menu di scelta rapida.  
  
4.  Verrà visualizzato un messaggio di conferma. Scegliere **Sì**.  
  
  
