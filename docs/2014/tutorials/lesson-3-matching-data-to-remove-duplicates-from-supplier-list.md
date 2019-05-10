---
title: "Lezione 3: Corrispondenza dei dati per rimuovere i duplicati dall'elenco fornitori | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c59a2fce106b08f53722ce44ae69225b680d7925
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484650"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>Lezione 3: Corrispondenza dei dati per rimuovere i duplicati dall'elenco fornitori
  Preparare la Knowledge Base per eseguire l'attività di corrispondenza creando criteri di corrispondenza nella Knowledge Base. In una Knowledge Base può essere presente solo un set di criteri di corrispondenza costituito da una o più regole di corrispondenza. Tramite una regola vengono identificati i domini coinvolti nel processo di corrispondenza e viene specificato il peso di ogni valore di dominio nella valutazione della corrispondenza. Nella regola specificare se i valori di dominio devono essere una corrispondenza esatta o se possono essere simili e indicare il livello di similitudine. Specificare inoltre se una corrispondenza di dominio è un prerequisito per il processo di corrispondenza. È possibile testare separatamente ogni regola, nonché tutti i criteri rispetto ai dati di esempio. Il processo di test consente di visualizzare i record i cui punteggi di corrispondenza sono maggiore di **punteggio record minimo** soglia specificato nella configurazione di DQS in un cluster (gruppo). È possibile continuare a modificare le regole nei criteri finché non si è soddisfatti.  
  
 Dopo aver definito i criteri, creare un progetto Data Quality per eseguire l'attività di corrispondenza. Il progetto corrispondente applica le regole di corrispondenza nei criteri di corrispondenza all'origine dati da valutare. Tramite questo processo viene valutata la probabilità che due righe coincidano. Quando DQS esegue l'analisi di corrispondenza, viene creato un cluster di record che DQS considera corrispondenze. Tramite DQS, uno dei record viene identificato in modo casuale come record pivot. È possibile verificare e rifiutare qualsiasi record che non è una corrispondenza appropriata per il cluster. Visualizzare [creare criteri di corrispondenza](https://msdn.microsoft.com/library/hh270290.aspx) per altre informazioni.  
  
 In questa lezione viene eseguita un'attività di corrispondenza per rimuovere i duplicati dall'elenco di fornitori. Innanzitutto, vengono creati i criteri di corrispondenza con una regola per identificare i duplicati nell'elenco di fornitori e pubblicare i criteri nella Knowledge Base. Successivamente, viene creato ed eseguito un progetto Data Quality per la corrispondenza. Infine, i risultati dell'attività di corrispondenza vengono esportati in un file di Excel che verrà utilizzato successivamente durante il caricamento dei dati in Master Data Services (MDS).  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 1: La definizione di criteri di corrispondenza](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  
