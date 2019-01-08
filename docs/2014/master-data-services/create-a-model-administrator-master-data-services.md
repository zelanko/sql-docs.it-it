---
title: Creare un amministratore di modelli (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6c0ef9c1b18c38b38ddefe900018bd0323956c88
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797673"
---
# <a name="create-a-model-administrator-master-data-services"></a>Creare un amministratore di modelli (Master Data Services)
  Nelle [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], creare un amministratore di modelli quando si desidera che un utente o gruppo affinché **Update** dell'autorizzazione per tutti gli oggetti in uno o più modelli.  
  
> [!TIP]  
>  Per semplificare l'amministrazione, creare un gruppo locale o di Windows e configurarlo come amministratore di modelli. È quindi possibile aggiungere e rimuovere utenti nel gruppo senza accedere a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione di accesso all'area funzionale **Autorizzazioni utenti e gruppi** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-model-administrator"></a>Per creare un amministratore del modello  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Autorizzazioni utenti e gruppi**.  
  
2.  Nella pagina **Utenti** o **Gruppi** selezionare la riga relativa all'utente o al gruppo che si desidera modificare.  
  
3.  Fare clic su **Modifica utente selezionato**.  
  
4.  Fare clic sulla scheda **Modelli** .  
  
5.  Facoltativamente selezionare un modello nell'elenco **Modello** .  
  
6.  Fare clic su **Modifica**.  
  
7.  Fare clic sul modello al quale si desidera concedere l'autorizzazione.  
  
8.  Nel menu, selezionare **Update**.  
  
9. Completare i passaggi 7 e 8 per ogni modello per cui si desidera che il gruppo o l'utente sia configurato come amministratore.  
  
10. Fare clic su **Salva**.  
  
## <a name="remarks"></a>Note  
 Non assegnare altre autorizzazioni a oggetti modello o membri della gerarchia. Se esegue l'operazione, l'utente non è più un amministratore e non è possibile visualizzare il modello in qualsiasi area funzionale diversa **Explorer**.  
  
 Vi è un'eccezione: se l'utente dispone **Update** le autorizzazioni assegnate a una gerarchia **radice** sul **membri della gerarchia** scheda, l'utente è ancora considerato un modello amministratore.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Autorizzazioni membri gerarchie &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
