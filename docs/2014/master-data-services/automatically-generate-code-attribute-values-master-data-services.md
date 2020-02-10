---
title: Generare automaticamente valori per l'attributo Code (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 9d6bdaf3e34ab6386cf4270c2610bd7b1a70e668
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483630"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Generare automaticamente valori per l'attributo Code (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] vengono automaticamente generati valori per l'attributo Code di un'entità quando si vuole che un valore intero venga assegnato automaticamente al valore Code ogni volta che si crea un nuovo membro.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Deve essere presente l'entità. Per altre informazioni, vedere [creare un'entità &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Per generare automaticamente valori Code  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Esplora modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare la riga per l'entità per cui si desidera generare codici.  
  
5.  Fare clic su **Modifica entità selezionata**.  
  
6.  Selezionare la casella di controllo **Crea valori Code automaticamente** .  
  
7.  Nella casella **Inizia con** digitare un numero da cui iniziare l'incremento. Se i membri esistono già, il valore Code verrà impostato in base al valore esistente più elevato. Ad esempio, se il valore Code esistente più elevato è 299, il valore Code del membro successivo sarà impostato su 300.  
  
8.  Fare clic su **Salva entità**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione automatica del codice &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [Generare automaticamente valori di attributo diversi dal codice &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
