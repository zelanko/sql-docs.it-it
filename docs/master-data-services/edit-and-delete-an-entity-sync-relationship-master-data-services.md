---
title: Modificare ed eliminare una relazione di sincronizzazione delle entità (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9a5e37f3-352e-45a6-b4a0-6f98f83b4bd8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 52ffe540d1afe9334533c2a5a8a631f342aed983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086458"
---
# <a name="edit-and-delete-an-entity-sync-relationship-master-data-services"></a>Modificare ed eliminare una relazione di sincronizzazione delle entità (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La sincronizzazione delle entità è una sincronizzazione unidirezionale e ripetibile tra le versioni dell'entità. Consente di condividere i dati delle entità tra i vari modelli. È possibile modificare ed eliminare una relazione di sincronizzazione creata.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Prerequisiti per modificare una relazione di sincronizzazione delle entità:  
  
-   È necessaria l'autorizzazione per accedere all'area funzionale Amministrazione sistema. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario essere un amministratore del modello per il modello di destinazione. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   È necessario avere almeno l'accesso in lettura all'entità di origine e a tutti i relativi attributi e membri.  
  
 Prerequisiti per eliminare una relazione di sincronizzazione delle entità:  
  
-   È necessaria l'autorizzazione per accedere all'area funzionale Amministrazione sistema. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario essere un amministratore del modello per il modello di destinazione. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Quando si modifica una relazione di sincronizzazione delle entità, tenere presente quanto segue:  
  
-   Le entità di origine e di destinazione devono essere in modelli diversi.  
  
-   Non deve essere stato eseguito il commit di una versione dell'entità di destinazione.  
  
-   Dopo aver stabilito una relazione di sincronizzazione, la destinazione viene immediatamente sincronizzata con l'origine.  
  
-   Una versione dell'entità di destinazione non può essere una versione dell'entità di origine di un'altra relazione di sincronizzazione.  
  
 Quando si esegue una relazione di sincronizzazione delle entità, tenere presente quanto segue:  
  
-   Verranno copiati solo i membri foglia.  
  
-   Gli attributi basati su dominio non verranno copiati.  
  
-   I membri temporaneamente eliminati non verranno copiati.  
  
-   La sincronizzazione non genera transazioni o cronologie dell'entità di destinazione.  
  
 **Per modificare una relazione di sincronizzazione delle entità**  
  
1.  In Gestione dati master fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entity Sync**(Sincronizzazione entità).  
  
3.  Nella pagina di **gestione della sincronizzazione delle entità** selezionare una relazione di sincronizzazione nella griglia.  
  
4.  Fare clic su **Modifica**. Viene visualizzato un riquadro sul lato destro.  
  
5.  Modificare il valore **Frequenza**. Selezionare **Sincronizza su richiesta**oppure **Auto Sync** (Sincronizzazione automatica) e impostare una frequenza.  
  
6.  Fare clic su **Salva**.  
  
 **Per eliminare una relazione di sincronizzazione delle entità**  
  
1.  In Gestione dati master fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entity Sync**(Sincronizzazione entità).  
  
3.  Nella pagina di **gestione della sincronizzazione delle entità** selezionare una relazione di sincronizzazione nella griglia.  
  
4.  Fare clic su **Elimina**.  
  
5.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare ed eseguire una relazione di sincronizzazione delle entità &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Relazione di sincronizzazione delle entità &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)  
  
  
