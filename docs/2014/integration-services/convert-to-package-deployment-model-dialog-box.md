---
title: Converti in finestra di dialogo del modello di distribuzione di pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dfe1f6e5b752284b6bb0feec96f4f3dfd67cc4f6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060345"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>Finestra di dialogo Converti in modello di distribuzione di pacchetti
  Con il comando **Converti nel modello di distribuzione del pacchetto** è possibile convertire un pacchetto nel modello di distribuzione del pacchetto dopo aver verificato la compatibilità del progetto e di ogni relativo pacchetto con questo modello. Se in un pacchetto vengono utilizzate funzionalità univoche per il modello di distribuzione del progetto, ad esempio parametri, il pacchetto non può essere convertito.  
  
## <a name="task-list"></a>Elenco attività  
 Per la conversione di un pacchetto nel modello di distribuzione del pacchetto sono necessari due passaggi.  
  
1.  Quando si seleziona il comando **Converti nel modello di distribuzione del pacchetto** dal menu **Progetto** viene verificata la compatibilità del progetto e di ogni relativo pacchetto con questo modello. I risultati vengono visualizzati nella tabella **Risultati** .  
  
     Se la verifica di compatibilità del progetto o di un pacchetto non viene completata correttamente, per ottenere ulteriori informazioni fare clic su **Non riuscito** nella colonna **Risultato** . Fare clic su **Salva report** per salvare una copia di queste informazioni in un file di testo.  
  
2.  Se il progetto e tutti i pacchetti superano la verifica di compatibilità, fare clic su **OK** per convertire il pacchetto.  
  
> [!NOTE]  
>  Per convertire un progetto nel modello di distribuzione del progetto usare la **Conversione guidata progetto di Integration Services**. Per altre informazioni, vedere [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [Distribuzione del pacchetto &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Conversione guidata progetto di Integration Services](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
