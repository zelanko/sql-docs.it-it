---
title: Gestione delle cache (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
author: minewiskan
ms.author: owend
ms.openlocfilehash: cdc5bcd2e0500749edfa298a871b6fec7243ddfb
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544983"
---
# <a name="managing-caches-xmla"></a>Gestione delle cache (XMLA)
  È possibile utilizzare il comando [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) in XML for Analysis (XMLA) per cancellare la cache di una dimensione o di una partizione specificata. Cancellare le forze della cache [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per ricompilare la cache per l'oggetto.  
  
## <a name="specifying-objects"></a>Specifica di oggetti  
 La proprietà [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `ClearCache` comando può contenere un riferimento a un oggetto solo per uno degli oggetti seguenti. Se un riferimento è relativo a un oggetto diverso da uno di quelli seguenti, si verifica un errore:  
  
 Database  
 Cancella la cache per tutte le dimensioni e le partizioni contenute nel database.  
  
 Dimension  
 Cancella la cache per la dimensione specificata.  
  
 Cube  
 Cancella la cache per tutte le partizioni contenute nei gruppi di misure per il cubo.  
  
 Gruppo di misure  
 Cancella la cache per tutte le partizioni contenute nel gruppo di misure.  
  
 Partizione  
 Cancella la cache per la partizione specificata.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
