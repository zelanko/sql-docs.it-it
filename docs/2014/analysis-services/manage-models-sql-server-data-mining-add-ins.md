---
title: Gestire i modelli (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, importing
- mining models, deleting
- mining models, managing
- mining models, training
- mining models, processing
- mining models, exporting
ms.assetid: c11380f0-7c24-4668-9cdf-9c53e4aff665
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d5f0619e7291cc08b1750c0b35f9639cb7a9872
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078042"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>Gestione modelli (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante Gestisci modelli, barra multifunzione Data Mining](media/dmc-manage.gif "pulsante Gestione modelli, barra multifunzione Data Mining")  
  
 Il **Gestione modelli** finestra di dialogo consente di interagire con i modelli di data mining esistente e strutture di data mining archiviati nel [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server a cui si è attualmente connessi. È inoltre possibile visualizzare e gestire strutture e modelli temporanei creati durante la connessione corrente. Se sono stati utilizzati sia modelli di sessione che modelli archiviati in un server, nella finestra di dialogo saranno visibili entrambi i tipi di modelli.  
  
## <a name="using-the-manage-models-wizard"></a>Utilizzo della procedura guidata Gestione modelli  
 Quando fa clic su **Gestione modelli**, il **gestire strutture e modelli** verrà visualizzata la finestra di dialogo, che fornisce accesso alle funzionalità seguenti per la gestione dei modelli di data mining e strutture esistenti:  
  
-   Ridenominazione di un modello o di una struttura di data mining  
  
-   Eliminazione di un modello o di una struttura di data mining  
  
-   Cancellazione di un modello o di una struttura di data mining  
  
-   Elaborazione di una struttura di data mining con dati nuovi o esistenti  
  
-   Esportazione o importazione di un modello o di una struttura di data mining  
  
> [!NOTE]  
>  Non è possibile creare query o modelli utilizzando questa finestra di dialogo. Per creare una nuova struttura di data mining, utilizzare una delle procedure guidate disponibili nel Client di Data Mining per Excel oppure utilizzare il **Editor avanzato di Query di Data Mining**.  
  
### <a name="requirements"></a>Requisiti  
 Per gestire i modelli di data mining, è innanzitutto necessario creare una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È necessaria una connessione anche se si stanno utilizzando modelli di sessione archiviati in un file temporaneo. Per altre informazioni su come creare o modificare una connessione, vedere [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Se l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a cui si è connessi non contiene strutture o modelli di data mining esistenti, sarà possibile crearli utilizzando le procedure guidate e altri strumenti disponibili in questo componente aggiuntivo. È anche possibile creare nuovi modelli utilizzando il **modello avanzato Editor di Data Mining**.  
  
## <a name="see-also"></a>Vedere anche  
 [Documentazione di modelli di Data Mining &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [Distribuzione e scalabilità di modelli di Data Mining &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
