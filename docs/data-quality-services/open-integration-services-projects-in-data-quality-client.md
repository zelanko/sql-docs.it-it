---
title: Aprire progetti di Integration Services in Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 23d86191b60cfe4dbcf6793b4765b51b7df66fc1
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591655"
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>Apertura di progetti di Integration Services nel client Data Quality

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Il componente DQS Cleansing in Integration Services consente di eseguire un progetto di pulizia in modalità batch. È tuttavia talvolta necessario rivedere i risultati della pulizia in un pacchetto di Integration Services in modo simile a quello utilizzato per rivedere i risultati della pulizia nella scheda **Gestisci e visualizza risultati** di un'attività di pulizia in un progetto Data Quality di DQS. DQS consente di aprire progetti di Integration Services in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] nello stesso modo in cui si apre qualsiasi altro progetto Data Quality dalla finestra di dialogo **Apri progetto** e di eseguire attività interattive sui risultati della pulizia in un progetto di Integration Services.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
  
-   Solo i progetti di Integration Services completati sono disponibili nella finestra di dialogo **Apri progetto** di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Nella finestra di dialogo **Apri progetto** non saranno disponibili progetti incompleti o in fase di esecuzione.  
  
-   I progetti di Integration Services vengono aperti nella fase di pulizia interattiva (scheda**Gestione vista e risultati** ) in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Non è possibile accedere alle schede **Pulisci** o **Mappa** . È possibile accedere solo alla scheda **Esporta** facendo clic su **Avanti**.  
  
-   Non è possibile eliminare un progetto di Integration Services bloccato da [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. È necessario procedere allo sblocco prima dell'eliminazione.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario avere completato correttamente l'esecuzione di un progetto di Integration Services che contenga un pacchetto con un componente di pulizia di DQS per poterlo visualizzare e aprire in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per aprire un progetto di Integration Services è necessario disporre del ruolo dqs_kb_editor o dqs_kb_operator nel database DQS_MAIN.  
  
  
##  <a name="Open"></a> Apertura di un progetto di Integration Services  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella pagina iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri progetto Data Quality**. Verrà visualizzata la finestra di dialogo **Apri progetto** .  
  
3.  Nella finestra di dialogo **Apri progetto** è possibile identificare un progetto di Integration Services in una delle modalità seguenti:  
  
    1.  **Nome progetto**: i progetti di Integration Services vengono elencati usando la terminologia di denominazione seguente: "Package.DQS Cleansing_*\<DATE>\<TIME>*_{GUID}." Ogni volta che si esegue correttamente lo stesso pacchetto in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], nella schermata **Apri progetto** è elencato un nuovo progetto.  
  
    2.  **Tipo di progetto**: i progetti di Integration Services presentano un tipo di progetto **SSIS** nella finestra di dialogo **Apri progetto**.  
  
     Selezionare un progetto, quindi fare clic su **Avanti**.  
  
4.  Il progetto di Integration Services viene aperto nella fase di pulizia interattiva (scheda**Gestione vista e risultati** ). È possibile eseguire una pulizia interattiva sui dati nel progetto di Integration Services. Per informazioni dettagliate sulla scheda **Gestisci e visualizza risultati**, vedere [Fase di pulizia interattiva](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) in [Pulizia di dati mediante DQS &#40;informazioni interne&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Fare clic su **Avanti** per passare alla scheda **Esporta** dove è possibile esportare i dati elaborati in una delle destinazioni seguenti: una nuova tabella nel database di SQL Server, un file CSV o un file di Excel. Per informazioni dettagliate sulla scheda **Esporta**, vedere [Fase di esportazione](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) in [Pulizia di dati mediante DQS &#40;informazioni interne&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
6.  Dopo avere esportato i dati, fare clic su **Fine** per chiudere il progetto di Integration Services.  

  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione DQS Cleansing](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Progetti di Integration Services (SSIS)](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
