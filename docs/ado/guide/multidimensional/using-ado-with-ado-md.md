---
title: Uso di ADO con ADO MD | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 69707e5026497a1f98ab168d71b4e6b286520fbe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194894"
---
# <a name="using-ado-with-ado-md"></a>Uso di ADO con ADO MD
ADO e ADO MD sono modelli a oggetti correlato ma separato. ADO fornisce gli oggetti per la connessione alle origini dati, l'esecuzione di comandi, il recupero di dati in formato tabulare e i metadati dello schema in un formato tabulare e visualizzazione di informazioni sugli errori del provider. ADO MD fornisce oggetti per il recupero di dati multidimensionali e visualizzazione dei metadati di schema multidimensionale.  
  
 Quando si lavora con un dati Multidimensionali, è possibile scegliere di utilizzare ADO, ADO MD o entrambi con l'applicazione. Facendo riferimento a entrambe le raccolte all'interno del progetto, si avrà accesso completo alle funzionalità fornite dai dati Multidimensionali.  
  
 È spesso utile per gli utenti ottenere una vista tabulare bidimensionale di un set di dati multidimensionale. Questo scopo, è possibile utilizzare l'oggetto ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto. Specificare l'origine per il [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) come la ***origine*** parametro per il [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo di un **Recordset**, piuttosto che come origine per un ADO MD **Cellset**.  
  
 Può anche essere utile visualizzare i metadati dello schema in una vista tabulare anziché come una gerarchia di oggetti. ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) metodo le [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto consente all'utente di aprire un **Recordset** che contiene le informazioni sullo schema. Il ***QueryType*** parametro delle **OpenSchema** metodo presenta numerosi [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valori correlati in modo specifico per provider di dati multidimensionali. I valori sono i seguenti:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Per usare i valori di enumerazione di ADO con ADO MD proprietà o metodi, il progetto deve fare riferimento a librerie ADO e di ADO MD. Ad esempio, è possibile usare l'oggetto ADO **adState** i valori di enumerazione con ADO MD [stato](../../../ado/reference/ado-md-api/state-property-ado-md.md) proprietà. Per altre informazioni su come stabilire i riferimenti alle librerie, vedere la documentazione dello strumento di sviluppo.  
  
 Per altre informazioni sui metodi e gli oggetti ADO, vedere la [riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (multidimensionale) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
