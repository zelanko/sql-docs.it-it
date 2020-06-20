---
title: Creare relazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 48c7956683258e1a9ae78a32eab0d02ff84c3b0a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939642"
---
# <a name="create-relationships"></a>Crea relazioni
  Utilizzare la finestra di dialogo **Crea relazioni** per modificare i mapping tra le colonne di origine e le colonne della tabella di ricerca configurati nell'Editor trasformazione Ricerca fuzzy, nell'Editor trasformazione Ricerca e nell'Editor trasformazione Ricerca termini.  
  
> [!NOTE]  
>  Quando viene richiamata dall'Editor trasformazione Ricerca termini, la finestra di dialogo **Crea relazioni** visualizza solo gli elenchi **Colonna di input** e **Colonna di ricerca** .  
  
 Per ulteriori informazioni sulle trasformazioni che utilizzano la finestra di dialogo **Crea relazioni** , vedere [Fuzzy Lookup Transformation](lookup-transformation.md), [Lookup Transformation](lookup-transformation.md)e [Term Lookup Transformation](term-lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili.  
  
 **Colonna di ricerca**  
 Consente di selezionare una colonna di ricerca nell'elenco delle colonne di ricerca disponibili.  
  
 **Tipo di mapping**  
 Consente di selezionare la corrispondenza fuzzy o esatta.  
  
 Quando si utilizza la corrispondenza fuzzy, le righe vengono considerate duplicati quando sono sufficientemente simili in tutte le colonne che hanno un tipo di corrispondenza fuzzy. Per ottenere i migliori risultati dalla corrispondenza fuzzy, è possibile specificare che alcune colonne devono utilizzare la corrispondenza esatta anziché la corrispondenza fuzzy. Ad esempio, se è noto che una determinata colonna non contiene errori o inconsistenze, è possibile specificare la corrispondenza esatta per tale colonna, in modo che vengano considerati come possibili duplicati solo le righe della colonna che contengono valori identici. Ciò migliora l'accuratezza della corrispondenza fuzzy nelle altre colonne.  
  
 **Flag di confronto**  
 Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](../comparing-string-data.md).  
  
 **Somiglianza minima**  
 Consente di impostare la soglia di somiglianza a livello di colonna utilizzando il dispositivo di scorrimento. Più il valore è prossimo a 1, più prossima deve essere la somiglianza del valore di ricerca con il valore di origine per essere qualificata come corrispondenza. L'aumento della soglia può incrementare la velocità di ricerca della corrispondenza in quanto viene considerato un minor numero di record candidati.  
  
 **Alias di output somiglianza**  
 Consente di specificare il nome per una nuova colonna di output che contiene i punteggi di somiglianza per la colonna selezionata. Se non si specifica un valore, la colonna di output non viene creata.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services-error-and-message-reference.md)   
 [Editor trasformazione Ricerca fuzzy &#40;scheda Colonne&#41;](../../fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor trasformazione Ricerca &#40;pagina Colonne&#41;](../../lookup-transformation-editor-columns-page.md)   
 [Editor trasformazione Ricerca termini &#40;scheda Ricerca termini&#41;](../../term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
