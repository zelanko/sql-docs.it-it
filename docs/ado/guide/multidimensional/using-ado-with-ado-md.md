---
title: Utilizzo di ADO con ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3c634ec056d42e97dcbea3422a0e19a33596d54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923141"
---
# <a name="using-ado-with-ado-md"></a>Uso di ADO con ADO MD
ADO e ADO MD sono modelli a oggetti correlati ma separati. ADO fornisce oggetti per la connessione a origini dati, l'esecuzione di comandi, il recupero di dati tabulari e metadati dello schema in formato tabulare e la visualizzazione delle informazioni sugli errori del provider. ADO MD fornisce oggetti per il recupero di dati multidimensionali e la visualizzazione di metadati dello schema multidimensionali.  
  
 Quando si lavora con una MDP, è possibile scegliere di usare ADO, ADO MD o entrambi con l'applicazione. Facendo riferimento a entrambe le librerie nel progetto, si avrà accesso completo alla funzionalità fornita da MDP.  
  
 Spesso è utile per i consumer ottenere una visualizzazione flat e tabulare di un set di dati multidimensionale. A tale scopo, è possibile utilizzare l'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ADO. Specificare l'origine per il set di [celle](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) come parametro di ***origine*** per il metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) di un recordset, anziché come origine per un **set**di **celle**ADO MD.  
  
 Potrebbe inoltre essere utile visualizzare i metadati dello schema in una vista tabulare anziché come una gerarchia di oggetti. Il metodo ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) sull'oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) consente all'utente di aprire un **Recordset** che contiene informazioni sullo schema. Il parametro ***QueryType*** del metodo **OpenSchema** presenta diversi valori [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) che si riferiscono in modo specifico a MDPs. I valori sono i seguenti:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Per usare i valori di enumerazione ADO con ADO MD proprietà o metodi, il progetto deve fare riferimento alle librerie ADO e ADO MD. È ad esempio possibile utilizzare i valori di enumerazione ADO **adState** con la proprietà ADO MD [state](../../../ado/reference/ado-md-api/state-property-ado-md.md) . Per ulteriori informazioni su come stabilire i riferimenti alle librerie, vedere la documentazione dello strumento di sviluppo.  
  
 Per ulteriori informazioni sugli oggetti e sui metodi ADO, vedere il [riferimento all'API ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (multidimensionale) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
