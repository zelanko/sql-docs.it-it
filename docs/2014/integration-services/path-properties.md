---
title: Proprietà percorso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc13943df93acf2227b089b177cdca6c86ee1831
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056656"
---
# <a name="path-properties"></a>Proprietà del percorso
  Gli oggetti flusso di dati nel [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] modello a oggetti hanno proprietà comuni e proprietà personalizzate a livello di componente, input e output e colonne di input e colonne di output. Molte proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
 In questo argomento vengono elencate e descritte le proprietà personalizzate dei percorsi che connettono gli oggetti del flusso di dati.  
  
## <a name="path-properties"></a>Proprietà del percorso  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] un percorso che connette componenti nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 Nella tabella seguente vengono descritte le proprietà configurabili dei percorsi in un flusso di dati. Inoltre, il motore del flusso di dati assegna valori a proprietà di sola lettura aggiuntive che non sono elencate qui.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer (enumerazione)|Un valore che indica se un'annotazione deve essere visualizzata con il percorso sulla superficie dell'area di progettazione. I valori possibili sono `AsNeeded`, `SourceName`, `PathName` e `Never`. Il valore predefinito è `AsNeeded`.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|L'input associato al percorso.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|L'output associato al percorso.|  
  
## <a name="see-also"></a>Vedere anche  
 [Percorsi in Integration Services](data-flow/integration-services-paths.md)   
 [Proprietà comuni](../../2014/integration-services/common-properties.md)   
 [Proprietà personalizzate della trasformazione](data-flow/transformations/transformation-custom-properties.md)   
 [Proprietà del flusso di dati che è possibile impostare tramite espressioni](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
