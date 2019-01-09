---
title: Autorizzazioni per elementi foglia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c34e517cadb6f529cd0406ae84a09eefc13f9c25
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817803"
---
# <a name="leaf-permissions-master-data-services"></a>Autorizzazioni per elementi foglia (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Le autorizzazioni foglia si applicano ai valori di attributo per tutti i membri foglia di un'entità.  
  
 Per le entità senza gerarchie esplicite abilitate, l'assegnazione delle autorizzazioni all'elemento **Foglia** equivale all'assegnazione delle autorizzazioni all'entità.  
  
 **Note:**  
  
-   Le autorizzazioni foglia si applicano solo all'area funzionale **Visualizzatore** dell'interfaccia utente.  
  
-   Le autorizzazioni assegnate agli attributi **Name** e **Code** non sono applicate.  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Lettura**|L'utente può leggere i membri foglia e i relativi attributi.|  
|**Creare**|L'utente può creare i membri foglia e assegnare i valori di attributo durante la creazione.|  
|**Update**|L'utente può aggiornare i membri foglia e gli attributi.|  
|**Elimina**|L'utente può eliminare i membri foglia.|  
|**Nega**|Negare l'accesso ai membri foglia.|  
  
 Le autorizzazioni di lettura, creazione, aggiornamento ed eliminazione possono essere combinate. Quando vengono assegnate le autorizzazioni di creazione, aggiornamento ed eliminazione, l'autorizzazione di lettura viene assegnata automaticamente.  
  
## <a name="attribute-permissions"></a>Autorizzazioni per attributi  
 Le autorizzazioni per gli attributi si applicano ai valori degli attributi per l'entità specifica. Gli utenti che dispongono solo delle autorizzazioni per gli attributi non possono aggiungere o rimuovere membri.  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Lettura**|L'utente può leggere gli attributi.|  
|**Creare**|L'utente può assegnare valori durante la creazione di membri.|  
|**Update**|L'utente può aggiornare gli attributi.|  
|**Elimina**|Nessun effetto.|  
|**Nega**|L'attributo non viene visualizzato.<br /><br /> Nota: Non è possibile negare in modo esplicito l'accesso agli attributi Name e Code.|  
  
### <a name="example"></a>Esempio  
 Per l'entità Product, assegnare l'autorizzazione **Update** all'attributo Subcategory. Negare l'autorizzazione per tutti gli altri attributi.  
  
|nome|codice|Subcategory (Aggiornamento)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} Mountain Bikes|  
|Mountain-100|BK-M201|{5} Mountain Bikes|  
  
 Nel **Visualizzatore**è possibile aggiornare qualsiasi valore di attributo nella colonna Subcategory. Se non si dispone delle autorizzazioni per un attributo, l'attributo non viene visualizzato.  
  
> [!NOTE]  
>  In questo esempio, Subcategory è un attributo basato su dominio, basato sull'entità SubcategoryList. È possibile selezionare una sottocategoria diversa per Mountain-100, ma non è possibile aggiungere o eliminare membri dall'entità SubcategoryList.  
  
## <a name="see-also"></a>Vedere anche  
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
    
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Membri &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Attributi &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
