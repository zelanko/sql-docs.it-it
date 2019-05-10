---
title: Creare un attributo basato su dominio (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 296ace8d97269d80179d437b1033b92196d6adc5
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478978"
---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>Creare un attributo basato su dominio (componente aggiuntivo MDS per Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]gli amministratori possono creare un attributo basato su dominio per vincolare i valori in una colonna a un set di valori specifico.  
  
 I valori possono essere già presenti nel foglio di lavoro oppure possono derivare da un'entità esistente.  
  
> [!NOTE]  
>  Se gli utenti digitano un valore nella colonna vincolata, anziché selezionarlo nell'elenco, gli errori vengono visualizzati nella colonna **$InputStatus$** al momento della pubblicazione.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione di accesso alle aree funzionali **Amministrazione sistema** e **Visualizzatore** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   Il modello e l'entità devono esistere già.  
  
### <a name="to-perform-this-procedure"></a>Per eseguire questa procedura:  
  
1.  In Excel caricare l'entità contenente la colonna (attributo) che si desiderare vincolare. Per altre informazioni, vedere [caricare i dati da MDS in Excel](export-data-to-excel-from-master-data-services.md).  
  
2.  Fare clic su una cella nella colonna che si desidera vincolare.  
  
3.  Nel gruppo **Compila modello** fare clic su **Proprietà attributi**.  
  
4.  Nella finestra di dialogo **Proprietà attributi** scegliere **Elenco vincolato (basato su dominio)** nell'elenco **Tipo di attributo**.  
  
5.  Nell'elenco **Popola l'attributo con valori di** :  
  
    -   Per usare valori del foglio di lavoro, scegliere **colonna selezionata**. Verranno create una nuova entità e una nuova tabella di staging con i valori dalla colonna selezionata.  
  
    -   Per utilizzare valori di un'entità esistente, scegliere il nome dell'entità.  
  
6.  Se si sceglie **colonna selezionata** nel passaggio precedente, nella casella **Nome nuova entità** digitare un nome per la nuova entità. Il nome può corrispondere a quello della colonna (attributo).  
  
7.  Fare clic su **OK**. In ogni cella nella colonna è ora presente un elenco di valori tra cui gli utenti possono scegliere.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Per aggiungere ed eliminare valori nell'elenco vincolato, caricare l'entità su cui l'attributo è basato. Per altre informazioni sul caricamento di entità, vedere [caricare i dati da MDS in Excel](export-data-to-excel-from-master-data-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi basati su dominio &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)   
 [Creare un'entità &#40;componente aggiuntivo MDS per Excel&#41;](create-an-entity-mds-add-in-for-excel.md)   
 [Compilazione di un modello &#40;componente aggiuntivo MDS per Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
