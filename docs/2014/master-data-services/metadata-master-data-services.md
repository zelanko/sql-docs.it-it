---
title: Metadati (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined metadata [Master Data Services], about user-defined metadata
- metadata [Master Data Services], about metadata
- metadata [Master Data Services]
- user-defined metadata [Master Data Services]
ms.assetid: ac1aabe3-d8d4-4d7a-8954-50ee3c185d81
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5f43034d81af8092a44c25db466fa8fa51b9eaa8
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961541"
---
# <a name="metadata-master-data-services"></a>Metadati (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] i metadati definiti dall'utente sono informazioni utilizzate per descrivere gli oggetti modello. È ad esempio possibile tenere traccia dei proprietari di un particolare modello o entità oppure dei sistemi di origine tramite cui vengono forniti dati a un'entità.  
  
 I metadati definiti dall'utente sono gestiti da un modello denominato **metadati**. Questo modello viene incluso automaticamente durante l' [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] installazione di ed è simile a tutti gli altri modelli MDS, ad eccezione del fatto che non è possibile crearne versioni.  
  
 Dopo aver popolato il modello Metadati con metadati definiti dall'utente, è possibile includerlo nelle viste sottoscrizioni, in modo che possa essere utilizzato dai sistemi di sottoscrizione.  
  
## <a name="metadata-entities"></a>Entità dei metadati  
 Nel modello Metadati sono incluse cinque entità, ognuna delle quali rappresenta un tipo di oggetto modello di dati master che supporta i metadati definiti dall'utente. L'entità di **definizione dei metadati del modello** , ad esempio, contiene membri che rappresentano modelli e l'entità di **definizione dei metadati dell'attributo** dispone di membri che rappresentano tutti gli attributi in tutti i modelli.  
  
 Per definire i metadati per un oggetto modello, è necessario popolare uno di questi attributi del membro. Nell'entità **definizione dei metadati dell'entità** , ad esempio, è possibile popolare l'attributo Description del membro Price con il testo: **il prezzo del prodotto quando è venduto a un cliente**.  
  
 I membri nel modello Metadati vengono aggiornati automaticamente ogni volta che gli oggetti modello che supportano i metadati definiti dall'utente vengono aggiunti o eliminati.  
  
 Non è possibile controllare la versione, aggiungere o modificare i flag di versione oppure salvare il modello Metadati come pacchetto di distribuzione. Tuttavia, sono disponibili le stesse funzionalità degli altri modelli di dati master. È ad esempio possibile implementare un set di regole business sul modello di metadati per applicare i criteri dati.  
  
## <a name="customizing-your-metadata-model"></a>Personalizzazione del modello dei metadati  
 Ciascuna entità di definizione dei metadati include gli attributi Name, Code e Description. È necessario creare attributi aggiuntivi per descrivere ulteriormente gli oggetti modello.  
  
 Può, ad esempio, essere necessario creare:  
  
-   Un attributo basato su dominio chiamato Owner da utilizzare per tenere traccia del proprietario di ciascun oggetto modello.  
  
-   Un attributo in formato libero chiamato Last Review Date da utilizzare per tenere traccia dell'ultima data in cui un oggetto è stato rivisto dal proprietario.  
  
-   Un attributo basato su dominio denominato Sources, che consente di tenere traccia e gestire i sistemi di origine che interagiscono con l' [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] istanza di.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Aggiungere metadati a un oggetto modello.|[Aggiungere metadati &#40;Master Data Services&#41;](add-metadata-master-data-services.md)
|&nbsp;|&nbsp;|
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Esportazione dei dati &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
