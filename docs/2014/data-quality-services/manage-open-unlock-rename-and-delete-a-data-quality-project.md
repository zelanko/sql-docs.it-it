---
title: Gestire (aprire, sbloccare, rinominare ed eliminare) un progetto Data Quality | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c77d1924bde3611bff4cf0328a659b2fea2cae45
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792354"
---
# <a name="manage-open-unlock-rename-and-delete-a-data-quality-project"></a>Gestione di un progetto Data Quality (apertura, sblocco, ridenominazione ed eliminazione)
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
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
     Alternativamente, è possibile aprire direttamente un progetto Data Quality elencato nell'area **Progetto Data Quality recente** facendo clic su di esso.  
  
3.  Nella finestra di dialogo **Apri progetto** fare clic per selezionare il progetto Data Quality che si desidera aprire, quindi fare clic su **Avanti**.  
  
4.  Il progetto Data Quality viene aperto nello stesso stato in cui era stata chiusa l'ultima volta l'attività. Un progetto Data Quality può presentare gli stati seguenti:  
  
    -   Per l'attività **Pulizia**, un progetto Data Quality può presentare gli stati seguenti: **Pulizia - Mappa**, **Pulizia - Pulisci**, **Pulizia - Gestisci e visualizza risultati** e **Pulizia - Esportazione**.  
  
    -   Per l'attività **Corrispondenza**, un progetto Data Quality può presentare gli stati seguenti: **Corrispondenza - Mappa**, **Corrispondenza - Corrispondenza**, **Corrispondenza - Sopravvivenza** e **Corrispondenza - Esportazione**.  
  
##  <a name="Unlock"></a> Sblocco di un progetto Data Quality  
 Quando viene creato, un progetto Data Quality è impostato in uno stato bloccato per impedire l'utilizzo o la modifica da parte di altri utenti. Se si desidera che altri utenti possano lavorare sul progetto Data Quality, una volta completate le proprie attività è necessario sbloccare il progetto. Per i progetti bloccati, viene visualizzato un simbolo a forma di lucchetto.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella schermata **Apri progetto** , fare clic con il pulsante destro del mouse su un progetto Data Quality bloccato che sia stato creato dall'utente corrente, quindi scegliere **Sblocca** dal menu di scelta rapida. Viene visualizzato un segno di spunta verde che indica che il progetto è ora sbloccato.  
  
##  <a name="Rename"></a> Ridenominazione di un progetto Data Quality  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella schermata **Apri progetto** , fare clic con il pulsante destro del mouse su un progetto Data Quality bloccato che sia stato creato dall'utente corrente, quindi scegliere **Rinomina** dal menu di scelta rapida.  
  
4.  Il nome del progetto Data Quality diventa modificabile nella colonna **Nome** . Digitare un nuovo nome e premere INVIO.  
  
##  <a name="Delete"></a> Eliminazione di un progetto Data Quality  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella schermata **Apri progetto** , fare clic con il pulsante destro del mouse su un progetto Data Quality sbloccato che sia stato creato dall'utente corrente, quindi scegliere **Elimina** dal menu di scelta rapida.  
  
4.  Verrà visualizzato un messaggio di conferma. Scegliere **Sì**.  
  
  
