---
title: Modificare un pacchetto di distribuzione di modelli | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6b0fdb7d-83dd-4392-9011-4ae642c471f1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 82f3e362643df17d9105ad6987a851211bd22865
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479505"
---
# <a name="edit-a-model-deployment-package"></a>Modificare un pacchetto di distribuzione di modelli
  Questo argomento descrive come distribuire parti selezionate di un modello in MDS, piuttosto che un modello intero. A tale scopo, modificare un pacchetto del modello MDS utilizzando l'Editor pacchetti di modelli.  
  
 La procedura guidata dell'Editor pacchetti di modelli consente di selezionare le entità specifiche, le gerarchie derivate, le viste delle sottoscrizioni e le regole business in un modello che si desidera includere in un pacchetto MDS e quindi successivamente effettuare la distribuzione. È possibile tralasciare quelle parti del modello che non si desidera distribuire. Quando si seleziona un'entità, anche tutti gli oggetti dipendenti di quell'entità vengono selezionati automaticamente.  
  
 Utilizzare l'Editor pacchetti di modelli per selezionare parti di un modello in un file di pacchetto creato dallo strumento MDSModelDeploy (che crea un file di pacchetto che include oggetti e dati) o la Distribuzione guidata modello (che crea un file che include solo la struttura del modello). Dopo avere modificato il modello nel pacchetto, utilizzare lo strumento MDSModelDeploy per distribuire oggetti e dati o la Distribuzione guidata modello per distribuire solo la struttura del modello.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che esista un pacchetto del modello da modificare. Per altre informazioni, vedere [Distribuzione di modelli &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md) e [Creare un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md) o [Creare un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
### <a name="to-edit-a-model-deployment-package"></a>Per modificare un pacchetto di distribuzione di modelli  
  
1.  In Esplora risorse sul server MDS, spostarsi in *drive*:\Program Files\Microsoft SQL Server\120\Master Data Services\Configuration.  
  
2.  Eseguire ModelPackageEditor.exe.  
  
3.  Nella procedura guidata dell'Editor pacchetti di modelli, fare clic su **Sfoglia**, spostarsi nella cartella che contiene i pacchetti, selezionare un pacchetto, quindi fare clic su **Apri**. Scegliere **Avanti**.  
  
4.  Selezionare quelle entità, gerarchie derivate, viste delle sottoscrizioni o regole business che si desidera distribuire. Deselezionare quelli che non si desidera distribuire. Scegliere **Avanti**.  
  
5.  Verificare l'elenco delle selezioni da distribuire. Per apportare modifiche, fare clic su **Indietro** e ripetizione il passaggio 4.  
  
6.  Fare clic su **Sfoglia**, spostarsi nella cartella nella quale si vuole salvare il pacchetto parziale, quindi immettere il nome file del pacchetto parziale (con estensione pkg). Fare clic su **Salva**.  
  
7.  Scegliere **Fine**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Distribuire un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
-   [Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
