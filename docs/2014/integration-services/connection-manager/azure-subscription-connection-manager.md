---
title: Gestione connessione della sottoscrizione di Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpsubscrconn.f1
- sql11.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6ea90d10a0228321d33a4c55076e9ed46a14c80c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58373810"
---
# <a name="azure-subscription-connection-manager"></a>Gestione connessione della sottoscrizione di Azure
  La gestione connessione Azure HDInsight consente a un pacchetto SSIS per connettersi a una sottoscrizione di Azure usando i valori specificati per la proprietà: ID sottoscrizione di Azure e certificato di gestione.  
  
1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** mostrata sopra selezionare **Sottoscrizione di Azure**, quindi fare clic su **Aggiungi**.  Viene visualizzata la finestra di dialogo **Editor gestione connessione di Sottoscrizione di Azure** .  
  
     ![SSIS-AzureSubscriptionManager](../media/ssis-azuresubscriptionmanager.png "SSIS-AzureSubscriptionManager")  
  
2.  Immettere l'ID sottoscrizione di Azure, che identifica in modo univoco una sottoscrizione di Azure, per **ID sottoscrizione di Azure**.  Il valore si trova nel [portale di gestione di Azure](https://manage.windowsazure.com) nella pagina **Impostazioni** :  
  
     ![SSIS-AzureSettings-SubscriptionID](../media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  Scegliere il **percorso dell'archivio** e il **nome dell'archivio** del certificato di gestione dagli elenchi a discesa.  
  
4.  Immettere l'**identificazione personale del certificato di gestione** oppure fare clic su **Sfoglia...** per scegliere un certificato dall'archivio selezionato. Il certificato deve essere caricato come certificato di gestione per la sottoscrizione. A tale scopo, fare clic su **Carica** nella pagina seguente del portale di Azure. Per altre informazioni, vedere questo [post MSDN](https://msdn.microsoft.com/library/azure/gg551722.aspx) .  
  
     ![SSIS-AzureSettings-ManagementCertificate](../media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  Fare clic su **Test connessione** per testare la connessione.  
  
6.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
  
