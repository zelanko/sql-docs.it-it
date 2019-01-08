---
title: Condizioni della regola di business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d5089921156f97509e157f771dbe20e1c33cf569
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355570"
---
# <a name="business-rule-conditions-master-data-services"></a>Condizioni della regola business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], le condizioni della regola business determinano le condizioni che devono essere true per una o più azioni da eseguire.  
  
> [!NOTE]  
>  Le condizioni sono facoltative. Se non si specifica una condizione, le azioni vengono eseguite ogni volta che i dati vengono convalidati rispetto alle regole business.  
  
## <a name="business-rule-conditions"></a>Condizioni della regola business  
  
|Nome condizione|Descrizione|  
|--------------------|-----------------|  
|**è uguale a**|L'attributo selezionato **è uguale a** un attributo specifico o a un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo, numerici, di data e di collegamento.|  
|**è diverso da**|L'attributo selezionato **è diverso da** un attributo specifico o da un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo, numerici, di data e di collegamento.|  
|**è maggiore di**|L'attributo selezionato **è maggiore di** un attributo specifico o di un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo, numerici e di data.|  
|**è maggiore o uguale a**|L'attributo selezionato **è maggiore o uguale a** un attributo specifico o a un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo, numerici e di data.|  
|**è minore di**|L'attributo selezionato **è minore di** un attributo specifico o di un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo, numerici e di data.|  
|**è minore o uguale a**|L'attributo selezionato **è minore o uguale a** un attributo specifico o a un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo, numerici e di data.|  
|**inizia con**|L'attributo selezionato **inizia con** un attributo specifico o un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo e di collegamento.|  
|**termina con**|L'attributo selezionato **termina con** un attributo specifico o un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo e di collegamento.|  
|**contiene**|L'attributo selezionato **contiene** un attributo specifico o un valore di attributo specifico oppure è vuoto.<br /><br /> Questa condizione è valida per valori di testo e di collegamento.|  
|**contiene il modello**|L'attributo selezionato **contiene il modello** di un attributo specifico o di un valore di attributo specifico oppure è vuoto. Utilizzare le espressioni regolari di .NET Framework per specificare il modello.<br /><br /> Per ulteriori informazioni su espressioni regolari, vedere [Elementi del linguaggio di espressioni regolari](https://go.microsoft.com/fwlink/?LinkId=164401) in MSDN Library.<br /><br /> Questa condizione è valida per valori di testo e di collegamento.|  
|**contiene il subset**|L'attributo selezionato **contiene il subset** di un attributo specifico o di un valore di attributo specifico. È necessario specificare la posizione iniziale per la ricerca (ad esempio 1 indica l'inizio della ricerca in corrispondenza del primo carattere).<br /><br /> Questa condizione è valida per valori di testo e di collegamento.|  
|**modificato**|L'attributo selezionato è stato **modificato** dall'ultima applicazione delle regole business al membro. È necessario specificare il gruppo di modifica di cui l'attributo è un membro.<br /><br /> Per altre informazioni sui gruppi di rilevamento modifiche, vedere [Aggiungere attributi a un gruppo rilevamento modifiche &#40;Master Data Services&#41;](add-attributes-to-a-change-tracking-group-master-data-services.md).<br /><br /> Questa condizione è valida per valori di testo, numerici, di data e di collegamento.|  
|**è compreso tra**|L'attributo selezionato **è compreso tra** due valori di attributo specifici.<br /><br /> Questa condizione è valida per valori di testo, numerici e di data.|  
  
> [!NOTE]  
>  Quando in una regola business è inclusa una condizione che consente di confrontare due valori e la regola viene applicata a un membro per il quale entrambi i valori sono NULL, la convalida eseguita dal membro in questione non verrà completata.  
  
## <a name="see-also"></a>Vedere anche  
 [Azioni Regola business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rule-actions-master-data-services.md)   
 [Regole business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Creare e pubblicare una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
