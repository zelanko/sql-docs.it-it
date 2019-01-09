---
title: Richiedere valori di attributo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3daebd23c88fe1865755fe4a24a672377fe077c8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765493"
---
# <a name="require-attribute-values-master-data-services"></a>Richiedere valori di attributo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]richiedere valori di attributo quando si desidera essere sicuri che i dati master siano completi.  
  
> [!NOTE]  
>  I membri a cui mancano valori di attributo basati su dominio non sono visualizzati nelle gerarchie derivate basate su tali relazioni.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-require-attribute-values"></a>Per richiedere valori di attributo  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Regole business** selezionare un modello nell'elenco a discesa **Modello** .  
  
4.  Nell'elenco a discesa **Entità** selezionare un'entità.  
  
5.  Nell'elenco a discesa **Tipi di membri** selezionare un tipo di membro a cui applicare la regola business.  
  
6.  Scegliere **Aggiungi**.  
  
7.  Nella casella **Nome** digitare un nome per la regola business.  
  
8.  Nel campo **Descrizione** digitare la descrizione aggiornata della regola business (facoltativo).  
  
9. Nel blocco **Then** fare clic su **Aggiungi**. Viene visualizzato un pannello.  
  
10. Nell'elenco a discesa **Operatore** selezionare **Azione richiesta**.  
  
11. Nell'elenco a discesa **Attributo** selezionare un attributo.  
  
12. Fare clic su **Salva**. Viene aggiunta una nuova riga alla griglia **Then** .  
  
13. Fare clic su **Salva**.  
  
14. Fare clic su **Pubblica tutto**.  
  
15. Nella finestra di dialogo di conferma, fare clic su **OK**. Il valore nella colonna **Stato della regola di business** è **Attiva**.  
  
## <a name="next-steps"></a>Next Steps  
  
-   Applicare regole business ai dati eseguendo una delle procedure riportate di seguito:  
  
    -   [Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Regole business &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Gerarchie derivate &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
