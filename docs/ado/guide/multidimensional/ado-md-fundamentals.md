---
title: Nozioni fondamentali su ADO MD | Microsoft Docs
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
ms.openlocfilehash: 690c7b58c336596485b9ade77f0c02928853cd2d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923206"
---
# <a name="ado-md-fundamentals"></a>Nozioni fondamentali su ADO MD
Microsoft® ActiveX® Data Objects (multidimensionale) (ADO MD) consente di accedere facilmente ai dati multidimensionali da linguaggi quali Microsoft Visual Basic® Microsoft Visual C++. ADO MD estende Microsoft ActiveX® Data Objects (ADO) per includere gli oggetti specifici di dati multidimensionali, ad esempio gli oggetti [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) e [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) . Con ADO MD è possibile esplorare uno schema multidimensionale, eseguire una query su un cubo e recuperare i risultati.  
  
 Come ADO, ADO MD USA un provider di OLE DB sottostante per ottenere l'accesso ai dati. Per lavorare con ADO MD, il provider deve essere un provider di dati multidimensionale (MDP) come definito dalla specifica OLE DB per OLAP. Un MDP presenta i dati nelle viste multidimensionali anziché nelle viste tabulari, che rappresenta il modo in cui un provider di dati tabulari (TDP) presenta i dati. Per ulteriori informazioni sulla sintassi e sul comportamento specifici supportati dal provider, vedere la documentazione relativa al provider di OLE DB OLAP.  
  
 In questo documento si presuppone una conoscenza approfondita del linguaggio di programmazione Visual Basic e una conoscenza generale di ADO e OLAP. Per ulteriori informazioni, vedere la [Guida per programmatori ADO](../../../ado/guide/ado-programmer-s-guide.md) e [OLE DB per l'elaborazione analitica in linea (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [Utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [Uso di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Guida per programmatori ADO](../../../ado/guide/ado-programmer-s-guide.md)   
 [Estensioni ADO per la sicurezza e il linguaggio di definizione dei dati (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Utilizzo di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
