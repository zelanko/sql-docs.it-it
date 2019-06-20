---
title: Nozioni di base di ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bbff704e174dd824eca7b1f71c8f9d3fc15def51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704421"
---
# <a name="ado-md-fundamentals"></a>Nozioni fondamentali su ADO MD
Microsoft® ActiveX® Data Objects (multidimensionale) (ADO MD) consente di accedere facilmente ai dati multidimensionali da linguaggi, ad esempio Microsoft Visual Basic®, Microsoft Visual C++®. ADO MD estende Microsoft ActiveX® dati Objects (ADO) per includere gli oggetti specifici di dati multidimensionali, ad esempio la [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) e [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetti. Con ADO MD si può esplorare schema multidimensionale, un cubo di query e recuperare i risultati.  
  
 Ad esempio ADO, ADO MD Usa un provider OLE DB sottostante per ottenere l'accesso ai dati. Per lavorare con ADO MD, il provider deve essere un provider di dati multidimensionali (dati Multidimensionali) come definito dalla specifica OLE DB per OLAP. Un MDP presenta i dati in visualizzazioni anziché alle viste tabulari, multidimensionali, ovvero come un provider di dati tabulare (TDP) presenta i dati. Vedere la documentazione per il provider OLE DB OLAP per altre informazioni sulla sintassi specifica e funzionalità supportate dal provider.  
  
 Questo documento presuppone una conoscenza approfondita del linguaggio di programmazione Visual Basic e una conoscenza generale di ADO e OLAP. Per altre informazioni, vedere la [Guida per programmatori ADO](../../../ado/guide/ado-programmer-s-guide.md) e [OLE DB per Online Analytical Processing (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [Utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [Uso di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Guida per programmatori ADO](../../../ado/guide/ado-programmer-s-guide.md)   
 [Estensioni ADO per Data Definition Language and Security (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Uso di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
