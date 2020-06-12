---
title: Unione di partizioni (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 65840066d3e95571db511a2015a1bee64aa8d922
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544953"
---
# <a name="merging-partitions-xmla"></a>Unione di partizioni (XMLA)
  Se le partizioni hanno la stessa struttura e progettazione delle aggregazioni, è possibile unire la partizione usando il comando [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) in XML for Analysis (XMLA). L'unione è un'azione particolarmente importante da eseguire quando si gestiscono partizioni, soprattutto per le partizioni che contengono dati cronologici partizionati in base alla data.  
  
 Un cubo finanziario può utilizzare ad esempio due partizioni:  
  
-   Una partizione rappresenta i dati finanziari per l'anno corrente utilizzando impostazioni di archiviazione OLAP relazionale (ROLAP) in tempo reale per motivi di prestazioni.  
  
-   Un'altra partizione contiene dati finanziari per gli anni precedenti utilizzando impostazioni di archiviazione OLAP multidimensionale (MOLAP) per l'archiviazione.  
  
 Entrambe le partizioni utilizzano impostazioni di archiviazione diverse, ma la stessa progettazione delle aggregazioni. Anziché elaborare il cubo attraverso anni di dati cronologici al termine dell'anno, è possibile utilizzare il comando `MergePartitions` per unire la partizione relativa all'anno corrente con quella relativa agli anni precedenti. In questo modo è possibile mantenere i dati aggregati senza che sia necessaria un'elaborazione completa del cubo che potrebbe richiedere molto tempo.  
  
## <a name="specifying-partitions-to-merge"></a>Specifica di partizioni da unire  
 Quando `MergePartitions` si esegue il comando, i dati di aggregazione archiviati nelle partizioni di origine specificate nella proprietà di [origine](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) vengono aggiunti alla partizione di destinazione specificata nella proprietà di [destinazione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla) .  
  
> [!NOTE]  
>  La proprietà `Source` può contenere più di un riferimento all'oggetto partizione, a differenza della proprietà `Target`.  
  
 Per essere unite, le partizioni specificate nelle proprietà `Source` e `Target` devono essere contenute dallo stesso gruppo di misure e devono utilizzare la stessa progettazione delle aggregazioni. In caso contrario si verifica un errore.  
  
 Le partizioni specificate in `Source` vengono eliminate dopo che il comando `MergePartitions` è stato completato correttamente.  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente vengono unite tutte le partizioni del gruppo di misure **Customer Counts** del cubo **Adventure Works** nel database di esempio **Adventure Works DW** nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] partizione **Customers_2004** .  
  
### <a name="code"></a>Codice  
  
```  
<MergePartitions xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
