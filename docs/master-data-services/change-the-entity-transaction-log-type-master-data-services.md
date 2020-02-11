---
title: Modificare il tipo di log delle transazioni dell'entità
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fde8e314462846088c7c673524d6e6d8d29ee631
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729669"
---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>Modificare il tipo di log delle transazioni dell'entità (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  È possibile modificare il tipo di log delle transazioni di un'entità in attributo, membro o nessuno.  
  
|Tipo di log delle transazioni|Descrizione|  
|--------------------------|-----------------|  
|Attributo|I log di modifica dell'entità vengono salvati al livello di attributo.<br /><br /> Il log delle transazioni viene salvato perché è per [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].|  
|Membro|I log di modifica dell'entità vengono salvati al livello di riga.<br /><br /> Tutte le modifiche dell'attributo attivano una nuova revisione di riga.<br /><br /> Quando si usa il tipo di log delle transazioni di riga, l'entità viene archiviata come dimensione a modifica lenta di tipo 4. Le viste sottoscrizione di tipo 2 e di tipo 4 (cronologia) sono supportate. Per altre informazioni, vedere [Formati di vista sottoscrizioni &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)<br /><br /> Fornisce prestazioni migliori.|  
|nessuno|Non vengono salvati log di modifica.<br /><br /> Fornisce le prestazioni migliori.|  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessaria l'autorizzazione per accedere all'area funzionale Amministrazione sistema. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Deve essere presente l'entità. Per altre informazioni, vedere [creare un'entità &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 **Per modificare il tipo di log delle transazioni**  
  
1.  In Gestione dati master fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Gestisci modello** selezionare la riga per il modello dell'entità da modificare, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestisci entità** selezionare la riga per l'entità da aggiornare, quindi fare clic su **Modifica**.  
  
4.  Scegliere il tipo di log delle transazioni nell'elenco a discesa.  
  
5.  Fare clic su **Salva**.  
  
  
