---
title: Utilizzo del drill-through per recuperare i dati di origine (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- queries [MDX], DRILLTHROUGH statement
- data retrieval [MDX]
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b437016cc29b2e4a85f781e3a422fb40c70f37c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074295"
---
# <a name="using-drillthrough-to-retrieve-source-data-mdx"></a>Utilizzo dell'istruzione DRILLTHROUGH per il recupero di dati di origine (MDX)
  Nel linguaggio MDX (Multidimensional Expressions) è disponibile l'istruzione [DRILLTHROUGH](/sql/mdx/mdx-data-manipulation-drillthrough), che consente di recuperare un set di righe dai dati di origine per una cella di un cubo.  
  
 Per eseguire un'istruzione `DRILLTHROUGH` su un cubo, è necessario definire un'azione drill-through per tale cubo. Per definire un'azione drill-through, in Progettazione cubi di [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]nel riquadro **Azioni** fare clic sul pulsante **Nuova azione drill-through**della barra degli strumenti. Nella nuova azione drill-through specificare il nome, la destinazione e la condizione dell'azione, nonché le colonne restituite dall'istruzione `DRILLTHROUGH`.  
  
## <a name="drillthrough-statement-syntax"></a>Sintassi dell'istruzione DRILLTHROUGH  
 La sintassi dell'istruzione `DRILLTHROUGH` è la seguente:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 La clausola `SELECT` identifica la cella del cubo che contiene i dati di origine da recuperare. Questa clausola `SELECT` è identica a una normale istruzione `SELECT` MDX, con la differenza che in questo caso nella clausola `SELECT` è possibile specificare solo un membro per ogni asse. Se su un asse sono specificati più membri, verrà generato un errore.  
  
 La sintassi `<Max_Rows>` specifica il numero massimo di righe in ogni set di righe restituito. Se il provider OLE DB utilizzato per connettersi all'origine dei dati non supporta `DBPROP_MAXROWS`, l'impostazione `<Max_Rows>` verrà ignorata.  
  
 La sintassi `<First_Rowset>` identifica la partizione il cui set di righe viene restituito per primo.  
  
 La sintassi `<Return_Columns>` identifica le colonne del database sottostante da restituire.  
  
## <a name="drillthrough-statement-example"></a>Esempio di istruzione DRILLTHROUGH  
 Nell'esempio seguente viene illustrato l'utilizzo dell'istruzione `DRILLTHROUGH`. In questo esempio l'istruzione DRILLTHROUGH esegue una query sugli elementi foglia delle dimensioni Store, Product e Time, lungo la dimensione Stores (l'asse di sezionamento), e quindi restituisce il gruppo di misure del reparto, l'ID del reparto e il nome del dipendente.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Manipolazione dei dati &#40;&#41;MDX](mdx-data-manipulation-manipulating-data.md)  
  
  
