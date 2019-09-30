---
title: Creare relazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fce60dd2a2663e23001805621e622b4334126a1e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291535"
---
# <a name="create-relationships"></a>Crea relazioni

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la finestra di dialogo **Crea relazioni** per modificare i mapping tra le colonne di origine e le colonne della tabella di ricerca configurati nell'Editor trasformazione Ricerca fuzzy, nell'Editor trasformazione Ricerca e nell'Editor trasformazione Ricerca termini.  
  
> [!NOTE]  
>  Quando viene richiamata dall'Editor trasformazione Ricerca termini, la finestra di dialogo **Crea relazioni** visualizza solo gli elenchi **Colonna di input** e **Colonna di ricerca** .  
  
 Per ulteriori informazioni sulle trasformazioni che utilizzano la finestra di dialogo **Crea relazioni** , vedere [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md), [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)e [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili.  
  
 **Colonna di ricerca**  
 Consente di selezionare una colonna di ricerca nell'elenco delle colonne di ricerca disponibili.  
  
 **Tipo di mapping**  
 Consente di selezionare la corrispondenza fuzzy o esatta.  
  
 Quando si utilizza la corrispondenza fuzzy, le righe vengono considerate duplicati quando sono sufficientemente simili in tutte le colonne che hanno un tipo di corrispondenza fuzzy. Per ottenere i migliori risultati dalla corrispondenza fuzzy, è possibile specificare che alcune colonne devono utilizzare la corrispondenza esatta anziché la corrispondenza fuzzy. Ad esempio, se è noto che una determinata colonna non contiene errori o inconsistenze, è possibile specificare la corrispondenza esatta per tale colonna, in modo che vengano considerati come possibili duplicati solo le righe della colonna che contengono valori identici. Ciò migliora l'accuratezza della corrispondenza fuzzy nelle altre colonne.  
  
 **Flag di confronto**  
 Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Somiglianza minima**  
 Consente di impostare la soglia di somiglianza a livello di colonna utilizzando il dispositivo di scorrimento. Più il valore è prossimo a 1, più prossima deve essere la somiglianza del valore di ricerca con il valore di origine per essere qualificata come corrispondenza. L'aumento della soglia può incrementare la velocità di ricerca della corrispondenza in quanto viene considerato un minor numero di record candidati.  
  
 **Alias di output somiglianza**  
 Consente di specificare il nome per una nuova colonna di output che contiene i punteggi di somiglianza per la colonna selezionata. Se non si specifica un valore, la colonna di output non viene creata.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor trasformazione Ricerca fuzzy &#40;scheda Colonne&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor trasformazione Ricerca &#40;scheda Colonne&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor trasformazione Ricerca termini &#40;scheda Ricerca termini&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
