---
title: 'Analysis Services tutorial-lezione 13: Distribuire | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 4e8e6bea11794545a2b0ab9c340e85344ec23d33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162189"
---
# <a name="deploy"></a>Distribuzione

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione si configurare proprietà di distribuzione; Specifica un server per distribuire e un nome per il modello. È quindi possibile distribuire il modello nel server. Dopo aver distribuito il modello, gli utenti possono connettersi a esso tramite un'applicazione client di creazione di report. Per altre informazioni, vedere [Distribuisci in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) e [distribuzione di soluzioni di modelli tabulari](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tempo stimato per il completamento della lezione: **5 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 12: Analizza in Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Se la distribuzione in Azure Analysis Services, è necessario disporre [le autorizzazioni di amministratore](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) sul serever.  

> [!IMPORTANT]  
> Se è installato il database di esempio AdventureWorksDW in un Server SQL in locale e si distribuisce il modello a un server Azure Analysis Services, un' [gateway dati locale](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) è obbligatorio.
  
## <a name="deploy-the-model"></a>Distribuire il modello  
  
#### <a name="to-configure-deployment-properties"></a>Per configurare le proprietà di distribuzione  

  
1.  Nella **Esplora soluzioni**, fare doppio clic il **AW Internet Sales** del progetto e quindi fare clic su **proprietà**.  
  
2.  Nel **pagine delle proprietà di AW Internet Sales** nella finestra di dialogo **Server di distribuzione**, nelle **Server** proprietà, immettere il nome completo del server. Se ci si connette ad Azure Analysis Services, nome del server deve includere l'URL completo.

    ![as-lesson13-deploy-property](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  Nel **Database** proprietà, digitare **Adventure Works Internet Sales**.  
  
4.  Nel **Model Name** proprietà, digitare **Adventure Works Internet Sales Model**.  
  
5.  Verificare le opzioni selezionate e fare clic su **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Per distribuire il modello Adventure Works Internet Sales
  
1.  Nella **Esplora soluzioni**, fare doppio clic il **AW Internet Sales** progetto > **compilare**.  

2.  Fare doppio clic il **AW Internet Sales** progetto > **Distribuisci**.

    Durante la distribuzione in Azure Analysis Services, potrebbe essere richiesto di immettere l'account. Immettere l'account aziendale e password, ad esempio nancy@adventureworks.com. Questo account deve essere incluso nel gruppo Admins nel server.
  
    Finestra di dialogo Distribuisci viene visualizzata e viene visualizzato lo stato di distribuzione dei metadati e ogni tabella inclusa nel modello.  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. Dopo aver completato la distribuzione, fare clic su **Chiudi**.  
  

In questa lezione descrive il metodo più semplice e più comune per distribuire un modello tabulare da SSDT. Le opzioni di distribuzione avanzata, ad esempio la procedura guidata distribuzione o l'automazione con XMLA e AMO offrono maggiore flessibilità, coerenza e le distribuzioni pianificate. Per altre informazioni, vedere [distribuzione di soluzioni di modelli tabulari](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).

## <a name="conclusion"></a>Conclusione  
La procedura è stata completata. Si è finito di creazione e distribuzione del primo modello tabulare di Analysis Services. Tramite questa esercitazione sono state completate le attività più comuni di creazione di un modello tabulare. Ora che il modello Adventure Works Internet Sales è stato distribuito, è possibile utilizzare SQL Server Management Studio per gestire il modello, nonché creare script di processo e un piano di backup. Gli utenti possono anche connettersi al modello usando un'applicazione client di creazione di report, ad esempio Microsoft Excel o Power BI.  

![come lesson13-ssms](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Argomenti successivi
[Connettersi con Power BI Desktop](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[Lezione supplementare: sicurezza dinamica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[Lezione supplementare: righe di dettaglio](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[Lezione supplementare: gerarchie incomplete](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
