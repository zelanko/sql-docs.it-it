---
title: Generare automaticamente valori per l'attributo Code
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ab9a9fbaac8875be535354a5f6f9122eb5089a0c
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813725"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Generare automaticamente valori per l'attributo Code (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] vengono automaticamente generati valori per l'attributo Code di un'entità quando si vuole che un valore intero venga assegnato automaticamente al valore Code ogni volta che si crea un nuovo membro.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Deve essere presente l'entità. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Per generare automaticamente valori Code  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Gestisci modello** selezionare la riga per il modello che contiene l'entità da modificare, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestisci entità** selezionare la riga per l'entità per cui generare codici, quindi fare clic su **Modifica**.  
  
4.  Selezionare la casella di controllo **Crea valori Code automaticamente** .  
  
5.  Nella casella **Inizia con** digitare un numero da cui iniziare l'incremento. Se i membri esistono già, il valore Code verrà impostato in base al valore esistente più elevato. Ad esempio, se il valore Code esistente più elevato è 299, il valore Code del membro successivo sarà impostato su 300.  
  
6.  Fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione automatica del codice &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [Generare automaticamente valori di attributi diversi da Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
