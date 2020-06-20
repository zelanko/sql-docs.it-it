---
title: "Lezione 3: corrispondenza dei dati per rimuovere i duplicati dall'elenco dei fornitori | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bdf3b71d985a60fed5080ec97462a43e79c4ca22
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054305"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>Lezione 3: Corrispondenza dei dati per rimuovere i duplicati dall'elenco fornitori
  Preparare la Knowledge Base per eseguire l'attività di corrispondenza creando criteri di corrispondenza nella Knowledge Base. In una Knowledge Base può essere presente solo un set di criteri di corrispondenza costituito da una o più regole di corrispondenza. Tramite una regola vengono identificati i domini coinvolti nel processo di corrispondenza e viene specificato il peso di ogni valore di dominio nella valutazione della corrispondenza. Nella regola specificare se i valori di dominio devono essere una corrispondenza esatta o se possono essere simili e indicare il livello di similitudine. Specificare inoltre se una corrispondenza di dominio è un prerequisito per il processo di corrispondenza. È possibile testare separatamente ogni regola, nonché tutti i criteri rispetto ai dati di esempio. Il processo di testing Visualizza i record i cui punteggi di corrispondenza sono maggiori della soglia del **punteggio record min** specificata nella configurazione DQS in un cluster (gruppo). È possibile continuare a modificare le regole nei criteri finché non si è soddisfatti.  
  
 Dopo aver definito i criteri, creare un progetto Data Quality per eseguire l'attività di corrispondenza. Il progetto corrispondente applica le regole di corrispondenza nei criteri di corrispondenza all'origine dati da valutare. Tramite questo processo viene valutata la probabilità che due righe coincidano. Quando DQS esegue l'analisi di corrispondenza, viene creato un cluster di record che DQS considera corrispondenze. Tramite DQS, uno dei record viene identificato in modo casuale come record pivot. È possibile verificare e rifiutare qualsiasi record che non è una corrispondenza appropriata per il cluster. Per ulteriori informazioni, vedere [l'argomento creare criteri di corrispondenza](https://msdn.microsoft.com/library/hh270290.aspx) .  
  
 In questa lezione viene eseguita un'attività di corrispondenza per rimuovere i duplicati dall'elenco di fornitori. Innanzitutto, vengono creati i criteri di corrispondenza con una regola per identificare i duplicati nell'elenco di fornitori e pubblicare i criteri nella Knowledge Base. Successivamente, viene creato ed eseguito un progetto Data Quality per la corrispondenza. Infine, i risultati dell'attività di corrispondenza vengono esportati in un file di Excel che verrà utilizzato successivamente durante il caricamento dei dati in Master Data Services (MDS).  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 1: Definizione di criteri di corrispondenza](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  
