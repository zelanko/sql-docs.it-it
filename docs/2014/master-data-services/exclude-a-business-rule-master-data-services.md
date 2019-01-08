---
title: Escludere una regola di business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6285d32ca514cacef4b78b31336bb33866baf860
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800703"
---
# <a name="exclude-a-business-rule-master-data-services"></a>Escludere una regola business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]escludere una regola di business quando non si vuole eliminarla in modo permanente, ma non si vuole convalidare i dati rispetto a essa.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-exclude-a-business-rule"></a>Per escludere una regola business  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Manutenzione regola business** selezionare un modello dall'elenco **Modello** .  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Dal **tipo di membro** selezionare un tipo di membro.  
  
6.  Dall'elenco **Attributo** selezionare un attributo o lasciare inalterata l'impostazione predefinita **Tutti**.  
  
7.  Nella griglia, nella riga relativa alla regola di business, selezionare la casella di controllo di **escludere** colonna. Il valore di **lo stato** colonna è **esclusione in sospeso**.  
  
8.  Fare clic su **Pubblica regole business**.  
  
9. Nella finestra di dialogo di conferma fare clic su **OK**. Il valore di **lo stato** colonna è **escluso**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [Creare e pubblicare una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regole di business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
