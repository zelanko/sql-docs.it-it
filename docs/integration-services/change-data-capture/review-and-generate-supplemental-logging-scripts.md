---
description: Rivedere e generare script di registrazione supplementare
title: Rivedere e generare script di registrazione supplementare | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- scripts
ms.assetid: 5c858ae2-37d6-42e8-a252-7f6ed4e628a7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 77a6b4f11ea2e01f43f1be335fad893ee87f1e90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457684"
---
# <a name="review-and-generate-supplemental-logging-scripts"></a>Rivedere e generare script di registrazione supplementare

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare la scheda **Scripts** per eseguire o rieseguire uno script nel database di origine Oracle per la configurazione della registrazione supplementare.  
  
 Prima di eseguire gli script selezionare una delle opzioni seguenti:  
  
 **Include changes in this session**  
 Selezionare questa opzione per eseguire lo script nelle nuove tabelle aggiunte all'istanza di CDC o in quelle modificate tramite l'editor delle proprietà.  
  
> [!NOTE]  
>  Se le tabelle dell'istanza di CDC non sono state modificate, lo script di registrazione supplementare Oracle sarà vuoto.  
  
 **Include all tables/capture instances**  
 Selezionare questa opzione per eseguire lo script in tutte le tabelle e le istanze di acquisizione dell'istanza di CDC.  
  
 Dopo avere selezionato una di queste opzioni, eseguire lo script di registrazione supplementare.  
  
### <a name="to-run-the-supplemental-logging-scripts"></a>Per eseguire gli script di registrazione supplementare  
  
1.  Fare clic su **Run Script** per eseguire lo script di registrazione supplementare nelle tabelle definite per l'istanza di CDC. Tramite questo script verranno scritte tutte le colonne di interesse nei log delle transazioni durante la registrazione delle operazioni UPDATE nelle tabelle acquisite. Lo script viene in genere esaminato ed eseguito da un amministratore di sistema Oracle.  
  
2.  Quando si eseguono gli script di registrazione supplementare, viene visualizzata la finestra di dialogo Oracle Credentials for Running Script in cui immettere un nome utente e una password Oracle validi. Per informazioni su come fornire le credenziali Oracle appropriate, vedere [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md).  
  
 Se necessario è anche possibile eseguire gli script manualmente tramite SQL\*Plus.  
  
### <a name="to-run-the-scripts-manually"></a>Per eseguire gli script manualmente  
  
1.  Scegliere **Copy** per incollare lo script negli Appunti. Aprire SQL* Plus e accedere alla directory contenente il database di origine Oracle. Incollare lo script in SQL\*Plus per eseguirlo.  
  
### <a name="to-save-the-supplemental-logging-script-in-a-text-file"></a>Per salvare lo script di registrazione supplementare in un file di testo  
  
1.  Scegliere **Save as** e accedere al percorso in cui si desidera salvare il file.  
  
2.  Assegnare un nome al file e scegliere **Save** per salvarlo.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di modifica delle proprietà dell'istanza di CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)  
  
  
