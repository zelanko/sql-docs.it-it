---
title: Modificare un'entità (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], changing name
ms.assetid: 6a5b9f14-6dfc-49d7-a771-e96461d4feae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cbf39fc0f0988a624d5a472b8938e47e4aa78a48
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62517806"
---
# <a name="edit-an-entity-master-data-services"></a>Modificare un'entità (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]è possibile modificare un'entità.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-edit-an-entity"></a>Per modificare un'entità  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Gestisci modelli** selezionare un modello dalla griglia, quindi fare clic su **Entità**.  
  
3.  Dalla griglia della pagina **Gestisci entità** selezionare la riga per l'entità da modificare, quindi fare clic su **Modifica**.  
  
4.  Nella casella **Nome** digitare il nome aggiornato dell'entità.  
  
5.  Nel campo **Descrizione** digitare la descrizione aggiornata dell'entità.  
  
6.  Nel campo **Nome per le tabelle di staging** digitare il nome aggiornato per la tabella di staging.  
  
7.  Per il campo **Tipo di log delle transazioni** scegliere il tipo di log delle transazioni aggiornato nell'elenco a discesa.  
  
     Per altre informazioni, vedere [Modificare il tipo di log delle transazioni dell'entità &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
8.  Selezionare o deselezionare la casella di controllo **Crea valori di codice automaticamente** .  
  
     Per altre informazioni, vedere [Creazione di codice automatica &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)  
  
9. Selezionare o deselezionare la casella di controllo **Abilita compressione dei dati** . La compressione di riga è attivata per impostazione predefinita.  
  
     Per altre informazioni, vedere [Data Compression](../relational-databases/data-compression/data-compression.md)  
  
## <a name="status"></a>Stato  
 La colonna Stato nella griglia mostra lo stato dell'operazione sull'entità. Quando si fa clic su **Salva entità**, viene visualizzata l'immagine seguente che indica che l'entità è in fase di aggiornamento.  
  
 ![Icona di aggiornamento dello stato](../master-data-services/media/mds-statusicon-updating.png "Icona di aggiornamento dello stato")  
  
 Se si verificano errori durante la creazione o la modifica di un'entità, viene visualizzata l'immagine seguente.  
  
 ![Icona di errore](../master-data-services/media/mds-statusicon-error.png "Icona di errore")  
  
 Quando lo stato è OK, viene visualizzata l'immagine seguente.  
  
 ![Icona dello stato OK](../master-data-services/media/mds-statusicon-ok.png "Icona dello stato OK")  
  
## <a name="see-also"></a>Vedere anche  
 [Gerarchie esplicite &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Eliminare un'entità &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)   
 [Entità &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
