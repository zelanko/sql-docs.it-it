---
title: 'Lezione 14: Distribuire | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96ffa6445d46f1e68efa907330d0945a499bf3b2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079135"
---
# <a name="lesson-14-deploy"></a>Lezione 14: Distribuzione
  In questa lezione verranno configurate proprietà di distribuzione, specificando un'istanza del server di distribuzione di Analysis Services in esecuzione in modalità tabulare e un nome per il modello distribuito. Si distribuirà quindi il modello nell'istanza. Dopo la distribuzione, gli utenti possono connettersi al modello utilizzando un'applicazione client di creazione di report. Per altre informazioni, vedere [Distribuzione di una soluzione del modello tabulare &#40;SSAS tabulare&#41;](tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
 Tempo stimato per il completamento della lezione: **5 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 13: Analizza in Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Distribuire il modello  
  
#### <a name="to-configure-deployment-properties"></a>Per configurare le proprietà di distribuzione  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **Adventure Works Internet Sales Tabular Model** e scegliere **Proprietà** dal menu di scelta rapida.  
  
2.  Nella finestra di dialogo **Deployment Tutorial Property Pages** (Pagine delle proprietà di Deployment Tutorial), in **Server di distribuzione**digitare il nome dell'istanza di Analysis Services in esecuzione in modalità tabulare nella proprietà **Server** . Si tratta dell'istanza in cui verrà distribuito il modello.  
  
    > [!IMPORTANT]  
    >  Per eseguire la distribuzione in un'istanza remota di Analysis Services, è necessario disporre delle autorizzazioni di amministratore.  
  
3.  Verificare i **modalità Query** è impostata su **In memoria**.  
  
    > [!NOTE]  
    >  Il modello creato tramite questa esercitazione non è supportato in modalità DirectQuery.  
  
4.  Nel **Database** proprietà, tipo `Adventure Works Internet Sales Model`.  
  
5.  Nel **cubo** proprietà del nome, tipo `Adventure Works Internet Sales Model`.  
  
6.  Verificare le opzioni selezionate e fare clic su **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Per distribuire il modello tabulare Adventure Works Internet Sales  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] scegliere **Deploy AW Internet Sales Tabular Model** (Distribuisci AW Internet Sales Tabular Model) dal menu **Compila**.  
  
     Verrà visualizzata la finestra di dialogo Distribuisci in cui sono indicati lo stato della distribuzione e ogni tabella inclusa nel modello.  
  
## <a name="conclusion"></a>Conclusione  
 La procedura è stata completata. La procedura di creazione e distribuzione del primo modello tabulare di Analysis Services è stata completata. Tramite questa esercitazione sono state completate le attività più comuni di creazione di un modello tabulare. Ora che il modello Adventure Works Internet Sales è stato distribuito, è possibile utilizzare SQL Server Management Studio per gestire il modello, nonché creare script di processo e un piano di backup. Gli utenti possono connettersi al modello utilizzando un'applicazione client di creazione report, ad esempio Microsoft Excel o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## <a name="additional-resources"></a>Risorse aggiuntive  
 Per altre informazioni sulle proprietà dei modelli tabulari che supportano i report [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], vedere [Proprietà report Power View &#40;SSAS tabulare&#41;](tabular-models/properties-ssas-tabular.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery &#40;SSAS tabulare&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Database modello tabulare &#40;SSAS tabulare&#41;](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
