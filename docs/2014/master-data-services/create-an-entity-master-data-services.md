---
title: Creare un'entità (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d85fc4c21f200bcdc5a489cfcee6b50bc9f4b98e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479910"
---
# <a name="create-an-entity-master-data-services"></a>Creare un'entità (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un'entità in cui siano contenuti i membri e i relativi attributi.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che sia presente un modello. Per altre informazioni, vedere [Creare un modello &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-master-data-services.md).  
  
### <a name="to-create-an-entity"></a>Per creare un'entità  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Fare clic su **Aggiungi entità**.  
  
5.  Nella casella **nome entità** Digitare il nome dell'entità.  
  
6.  Nella casella **nome per le tabelle di staging** Digitare un nome per la tabella di staging.  
  
    > [!TIP]  
    >  Usare il nome del modello come parte del nome della tabella di staging, ad esempio *Nomemodello_Nomeentità*. In questo modo risulta più agevole trovare le tabelle nel database. Per ulteriori informazioni sulle tabelle di staging, vedere [Data Import &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
7.  Facoltativa. Selezionare la casella di controllo **Crea valori Code automaticamente** . Per altre informazioni, vedere [Creazione di codice automatica &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md).  
  
8.  Dall'elenco **Abilita gerarchie esplicite e raccolte** , selezionare una delle opzioni seguenti:  
  
    -   **No**. Selezionare questa opzione se non è necessario abilitare l'entità per gerarchie esplicite e raccolte. È possibile modificare tale opzione in seguito, se necessario.  
  
    -   **Sì**. Selezionare questa opzione quando si desidera abilitare l'entità per gerarchie esplicite e raccolte. Digitare un nome nella casella **nome gerarchia esplicita** . Facoltativamente, selezionare **gerarchia obbligatoria (tutti i membri foglia sono inclusi** per rendere la gerarchia esplicita una gerarchia obbligatoria.  
  
9. Fare clic su **Salva entità**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Creare un attributo di testo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [Creare un attributo basato su dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [Creare un attributo di file &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Entità &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [Gerarchie esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [Modificare il nome di un'entità &#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [Eliminare un'entità &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  
