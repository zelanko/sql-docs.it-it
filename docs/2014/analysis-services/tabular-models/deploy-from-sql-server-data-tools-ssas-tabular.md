---
title: Eseguire la distribuzione da SQL Server Data Tools (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1690e2772de50258a69a4a33b048f16f7da2caca
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939718"
---
# <a name="deploy-from-sql-server-data-tools-ssas-tabular"></a>Distribuire da SQL Server Data Tools (SSAS tabulare)
  Utilizzare le attività contenute in questo argomento per distribuire una soluzione del modello tabulare utilizzando il comando Distribuisci in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Sezioni dell'argomento:  
  
-   [Configurare le proprietà opzioni di distribuzione e server di distribuzione](#bkmk_deploy)  
  
-   [Distribuire una soluzione del modello tabulare](#bkmk_deploy_proc)  
  
-   [Stato distribuzione](#bkmk_deploy_status)  
  
##  <a name="configure-deployment-options-and-deployment-server-properties"></a><a name="bkmk_deploy"></a>Configurare le proprietà opzioni di distribuzione e server di distribuzione  
 Prima di distribuire tale soluzione, è necessario innanzitutto specificare le proprietà Opzioni di distribuzione e Server di distribuzione. Per altre informazioni sulle impostazioni e le proprietà di distribuzione, vedere [Distribuzione di una soluzione del modello tabulare &#40;SSAS tabulare&#41;](tabular-model-solution-deployment-ssas-tabular.md).  
  
#### <a name="to-configure-deployment-options-and-deployment-server-properties"></a>Per configurare le proprietà Opzioni di distribuzione e Server di distribuzione  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]Esplora soluzioni **di**fare clic con il pulsante destro del mouse sul nome del progetto, quindi scegliere **Proprietà**.  
  
2.  In **Opzioni di distribuzione**della finestra di dialogo ** \<project name> Proprietà** specificare le impostazioni delle proprietà se diverse dalle impostazioni predefinite.  
  
    > [!NOTE]  
    >  Per i modelli in modalità cache, in corrispondenza di **Modalità query** è sempre selezionata l'opzione **In-Memory**.  
  
    > [!NOTE]  
    >  Non è possibile specificare **Impostazioni di rappresentazione** per i modelli in modalità DirectQuery.  
  
3.  In **Server di distribuzione**specificare le impostazioni delle proprietà **Server** (nome), **Edizione**, **Database** (nome) e **Nome cubo** , se diverse dalle impostazioni predefinite, quindi fare clic su **OK**.  
  
> [!NOTE]  
>  È inoltre possibile specificare l'impostazione della proprietà Server di distribuzione predefinito in modo che tutti i nuovi progetti creati vengano distribuiti automaticamente nel server specificato. Per altre informazioni, vedere [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](properties-ssas-tabular.md).  
  
##  <a name="deploy-a-tabular-model-solution"></a><a name="bkmk_deploy_proc"></a>Distribuire una soluzione di modello tabulare  
  
#### <a name="to-deploy-a-tabular-model-solution"></a>Per distribuire una soluzione del modello tabulare  
  
-   In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] scegliere **Distribuisci \<project name> **dal menu **Compila** .  
  
     Verrà visualizzata la finestra di dialogo **Distribuisci** e verrà fornita l'indicazione dello stato della distribuzione dei metadati e dell'elaborazione di ogni tabella inclusa nel modello, a meno che la proprietà Opzione di elaborazione non sia impostata su Non elaborare. Una volta completato il processo di distribuzione, utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per connettersi all'istanza di Analysis Services e verificare il nuovo oggetto di database modello creato. In alternativa, utilizzare un'applicazione client di creazione report per connettersi al modello distribuito.  
  
##  <a name="deploy-status"></a><a name="bkmk_deploy_status"></a>Stato distribuzione  
 La finestra di dialogo **Distribuisci** consente di monitorare lo stato di un'operazione di distribuzione. Inoltre è possibile arrestare un'operazione di distribuzione.  
  
 **Status**  
 Viene indicato se l'operazione di distribuzione ha avuto esito positivo o negativo.  
  
 **Dettagli**  
 Vengono elencati gli elementi dei metadati distribuiti, lo stato di ogni elemento dei metadati e viene fornito un messaggio relativo a eventuali problemi.  
  
 **Arresta distribuzione**  
 Fare clic su questa opzione per arrestare l'operazione di distribuzione. Questa opzione è utile se l'operazione di distribuzione è troppo lunga o se si sono verificati troppi errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di soluzioni di modelli tabulari &#40;SSAS tabulare&#41;](tabular-model-solution-deployment-ssas-tabular.md)   
 [Configurare la modellazione dei dati e le proprietà di distribuzione predefinite &#40;SSAS tabulare&#41;](properties-ssas-tabular.md)  
  
  
