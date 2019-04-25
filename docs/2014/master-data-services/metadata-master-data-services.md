---
title: Metadati (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined metadata [Master Data Services], about user-defined metadata
- metadata [Master Data Services], about metadata
- metadata [Master Data Services]
- user-defined metadata [Master Data Services]
ms.assetid: ac1aabe3-d8d4-4d7a-8954-50ee3c185d81
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f45d9d2a50327259c987cd41fefc6039c629eb77
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62764702"
---
# <a name="metadata-master-data-services"></a>Metadati (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] i metadati definiti dall'utente sono informazioni utilizzate per descrivere gli oggetti modello. È ad esempio possibile tenere traccia dei proprietari di un particolare modello o entità oppure dei sistemi di origine tramite cui vengono forniti dati a un'entità.  
  
 Metadati definiti dall'utente sono gestiti da un modello chiamato **metadati**. Questo modello viene incluso automaticamente durante [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] è installato, ed è simile a tutti gli altri modelli MDS, ad eccezione del fatto che non è possibile creare le relative versioni.  
  
 Dopo aver popolato il modello Metadati con metadati definiti dall'utente, è possibile includerlo nelle viste sottoscrizioni, in modo che possa essere utilizzato dai sistemi di sottoscrizione.  
  
## <a name="metadata-entities"></a>Entità dei metadati  
 Nel modello Metadati sono incluse cinque entità, ognuna delle quali rappresenta un tipo di oggetto modello di dati master che supporta i metadati definiti dall'utente. Ad esempio, il **definizione metadati modello** entità contiene membri che rappresentano modelli e il **definizione metadati attributo** entità contiene membri che rappresentano tutti gli attributi in tutti i modelli.  
  
 Per definire i metadati per un oggetto modello, è necessario popolare uno di questi attributi del membro. Ad esempio, nelle **definizione metadati entità** entità, è possibile popolare l'attributo Description del membro Price con il testo: **Il prezzo del prodotto quando è venduto a un cliente**.  
  
 I membri nel modello Metadati vengono aggiornati automaticamente ogni volta che gli oggetti modello che supportano i metadati definiti dall'utente vengono aggiunti o eliminati.  
  
 Non è possibile controllare la versione, aggiungere o modificare i flag di versione oppure salvare il modello Metadati come pacchetto di distribuzione. Tuttavia, sono disponibili le stesse funzionalità degli altri modelli di dati master. È ad esempio possibile implementare un set di regole business sul modello di metadati per applicare i criteri dati.  
  
## <a name="customizing-your-metadata-model"></a>Personalizzazione del modello dei metadati  
 Ciascuna entità di definizione dei metadati include gli attributi Name, Code e Description. È necessario creare attributi aggiuntivi per descrivere ulteriormente gli oggetti modello.  
  
 Può, ad esempio, essere necessario creare:  
  
-   Un attributo basato su dominio chiamato Owner da utilizzare per tenere traccia del proprietario di ciascun oggetto modello.  
  
-   Un attributo in formato libero chiamato Last Review Date da utilizzare per tenere traccia dell'ultima data in cui un oggetto è stato rivisto dal proprietario.  
  
-   Un attributo basato su dominio denominato Sources da utilizzare per tenere traccia e gestire i sistemi di origine che interagiscono con il [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] istanza.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Aggiungere metadati a un oggetto modello.|[Aggiungere metadati &#40;Master Data Services&#41;](add-metadata-master-data-services.md)
|&nbsp;|&nbsp;|
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Esportazione di dati &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
