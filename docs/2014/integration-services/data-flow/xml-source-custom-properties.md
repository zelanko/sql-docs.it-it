---
title: Proprietà personalizzate dell'origine XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0e4f6ad2be4f2253ad09403231fca01a0996bd2f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429868"
---
# <a name="xml-source-custom-properties"></a>Proprietà personalizzate dell'origine XML
  L'origine XML include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine XML. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modalità utilizzata per accedere ai dati XML.|  
|UseInlineSchema|Boolean|Valore che indica se utilizzare una definizione dello schema inline all'interno dell'origine XML. Il valore predefinito di questa proprietà è `False`.|  
|XMLData|string|File o variabili da cui recuperare i dati XML.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
|XMLSchemaDefinition|string|Percorso e nome del file di definizione dello schema (estensione xsd).<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'output dell'origine XML. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|RowsetID|string|Valore che identifica il set di righe associato all'output.|  
  
 Le colonne di output dell'origine XML non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Origine XML](xml-source.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
