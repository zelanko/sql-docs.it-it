---
title: Proprietà dell'origine OData | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19b7bf852fcebd390d3659fcd2bff53fa0446d0c
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045054"
---
# <a name="odata-source-properties"></a>Proprietà dell'origine OData
Quando si fa clic con il pulsante destro del mouse su **Origine OData** nel flusso di dati e si sceglie **Proprietà**, vengono visualizzate le proprietà del componente **Origine OData** nella finestra **Proprietà**.  

## <a name="properties"></a>Proprietà 

|Proprietà|Descrizione|  
|-|-|  
|CollectionName|Nome della raccolta da recuperare dal servizio OData. La proprietà **CollectionName** viene utilizzata quando **UseResourcePath** è False.<br /><br /> Questa proprietà ammette le espressioni e consente l'impostazione del valore in fase di esecuzione. Tuttavia, se i metadati della raccolta non corrispondono a quelli esistenti in fase di progettazione, si verifica un errore di convalida e l'esecuzione del flusso di dati non viene completata.|  
|DefaultStringLength|Con questo valore viene specificata la lunghezza predefinita per le colonne stringa che sono prive della lunghezza massima.<br /><br /> **Default:** 4.000|  
|Query|Parametri della query OData. Questa proprietà ammette le espressioni e può essere impostata in fase di esecuzione.|  
|ResourcePath|Utilizzare questa proprietà quando è necessario specificare un percorso completo della risorsa, anziché selezionare semplicemente il nome di una raccolta. Questa proprietà viene utilizzata quando **UseResourcePath** è True.|  
|UseResourcePath|Quando impostato su True, il valore di **ResourcePath** viene aggiunto all'URL di base per determinare il percorso del feed OData. Quando impostato su False, viene utilizzato il valore di **CollectionName** .<br /><br /> **Default:** False|  
  
## <a name="see-also"></a>Vedere anche
[Origine OData](odata-source.md)
