---
title: 'Lezione 13: Distribuire | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c20a0367612aee48c1a58e9cde8ba1a44d3fafc
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404803"
---
# <a name="lesson-13-deploy"></a>Lezione 13: Distribuzione
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione verranno configurate le proprietà di distribuzione; specificare un locale o istanza del server di Azure e un nome per il modello. Il modello verrà quindi distribuita per quell'istanza. Dopo aver distribuito il modello, gli utenti possono connettersi a esso tramite un'applicazione client di creazione di report. Per altre informazioni sulla distribuzione, vedere [distribuzione di soluzioni di modelli tabulari](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md) e [Distribuisci in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Tempo stimato per il completamento della lezione: **5 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 12: Analizza in Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Distribuire il modello  
  
#### <a name="to-configure-deployment-properties"></a>Per configurare le proprietà di distribuzione  
  
1.  Nella **Esplora soluzioni**, fare doppio clic il **AW Internet Sales** del progetto e quindi fare clic su **proprietà**.  
  
2.  Nel **pagine delle proprietà di AW Internet Sales** nella finestra di dialogo **Server di distribuzione**, nel **Server** proprietà, digitare il nome di un server Azure Analysis Services o un oggetto istanza del server in locale in esecuzione in modalità tabulare. Questo sarà l'istanza del server che verrà distribuito il modello.  

    ![aas-deploy-deployment-server-property](media/aas-deploy-deployment-server-property.png)
 
    > [!IMPORTANT]  
    > Il remoto Analysis Services istanza nell'ordine eseguire la distribuzione, è necessario disporre delle autorizzazioni di amministratore.  
  
3.  Nel **Database** proprietà, digitare **Adventure Works Internet Sales**.  
  
4.  Nel **Model Name** proprietà, digitare **Adventure Works Internet Sales Model**.  
  
5.  Verificare le opzioni selezionate e fare clic su **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Per distribuire il modello tabulare Adventure Works Internet Sales  
  
1.  Nella **Esplora soluzioni**, fare doppio clic il **AW Internet Sales** progetto > **compilare**.  

2.  Fare doppio clic il **AW Internet Sales** progetto > **Distribuisci**.

    Durante la distribuzione in Azure Analysis Services, sarà probabilmente richiesto di immettere l'account. Immettere l'account aziendale e password, ad esempio nancy@adventureworks.com. Questo account deve essere incluso nel gruppo Admins nell'istanza del server.
  
    Verrà visualizzata la finestra di dialogo Distribuisci in cui sono indicati lo stato della distribuzione e ogni tabella inclusa nel modello.  
    
    ![aas-deploy-status](media/aas-deploy-status.png)
  
3. Dopo aver completato la distribuzione, fare clic su **Chiudi**.  
  
## <a name="conclusion"></a>Conclusione  
La procedura è stata completata. Si è finito di creazione e distribuzione del primo modello tabulare di Analysis Services. Tramite questa esercitazione sono state completate le attività più comuni di creazione di un modello tabulare. Ora che il modello Adventure Works Internet Sales è stato distribuito, è possibile utilizzare SQL Server Management Studio per gestire il modello, nonché creare script di processo e un piano di backup. Gli utenti possono anche connettersi al modello usando un'applicazione client di creazione di report, ad esempio Microsoft Excel o Power BI.  

![as-tabular-lesson13-ssms](media/as-tabular-lesson13-ssms.png)
  
  
## <a name="see-also"></a>Vedere anche  
[Modalità DirectQuery](../tabular-models/directquery-mode-ssas-tabular.md)  
[Configurare la modellazione dei dati e le proprietà di distribuzione predefinite](../tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[Database modello tabulare](../tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  ## <a name="whats-next"></a>Quali sono le operazioni successive?
*  [Lezione supplementare: implementare la sicurezza dinamica mediante i filtri di riga](supplemental-lesson-implement-dynamic-security-by-using-row-filters.md).

*  [Supplementare lezione - configurare le proprietà di creazione di report per i report Power View](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md).
