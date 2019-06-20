---
title: Unione di partizioni (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 419ebd0d67b65213fde7393430aedec14249b2ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63261635"
---
# <a name="merging-partitions-xmla"></a>Unione di partizioni (XMLA)
  Se le partizioni hanno la stessa progettazione delle aggregazioni e struttura, è possibile unire la partizione tramite il [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) comando XML for Analysis (XMLA). L'unione è un'azione particolarmente importante da eseguire quando si gestiscono partizioni, soprattutto per le partizioni che contengono dati cronologici partizionati in base alla data.  
  
 Un cubo finanziario può utilizzare ad esempio due partizioni:  
  
-   Una partizione rappresenta i dati finanziari per l'anno corrente utilizzando impostazioni di archiviazione OLAP relazionale (ROLAP) in tempo reale per motivi di prestazioni.  
  
-   Un'altra partizione contiene dati finanziari per gli anni precedenti utilizzando impostazioni di archiviazione OLAP multidimensionale (MOLAP) per l'archiviazione.  
  
 Entrambe le partizioni utilizzano impostazioni di archiviazione diverse, ma la stessa progettazione delle aggregazioni. Invece di elaborare il cubo attraverso anni di dati cronologici alla fine dell'anno, è possibile usare la **MergePartitions** comando per unire la partizione per l'anno corrente della partizione degli anni precedenti. In questo modo è possibile mantenere i dati aggregati senza che sia necessaria un'elaborazione completa del cubo che potrebbe richiedere molto tempo.  
  
## <a name="specifying-partitions-to-merge"></a>Specifica di partizioni da unire  
 Quando la **MergePartitions** comando viene eseguito, i dati aggregati archiviati nelle partizioni di origine specificate nel [origine](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) viene aggiunta alla partizione di destinazione specificata nella proprietà di [destinazione ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla) proprietà.  
  
> [!NOTE]  
>  Il **origine** proprietà può contenere più di un riferimento all'oggetto partizione. Tuttavia, il **destinazione** non è di proprietà.  
  
 Per essere unite, le partizioni specificate in entrambe le **origine** e **destinazione** deve essere incluso nello stesso gruppo di misure e usare la stessa progettazione delle aggregazioni. In caso contrario si verifica un errore.  
  
 Le partizioni specificate nella **origine** vengono eliminati dopo il **MergePartitions** comando viene completato correttamente.  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 L'esempio seguente unisce tutte le partizioni del **Customer Counts** gruppo di misure del **Adventure Works** cubo la **Adventure Works DW** esempio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di database nel **Customers_2004** partizione.  
  
### <a name="code"></a>Codice  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
