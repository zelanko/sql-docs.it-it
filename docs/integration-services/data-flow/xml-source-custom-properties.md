---
description: Proprietà personalizzate dell'origine XML
title: Proprietà personalizzate dell'origine XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f77a63b11636f2be16e3d7c81c5b902a95b2a84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425593"
---
# <a name="xml-source-custom-properties"></a>Proprietà personalizzate dell'origine XML

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'origine XML include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine XML. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modalità utilizzata per accedere ai dati XML.|  
|UseInlineSchema|Boolean|Valore che indica se utilizzare una definizione dello schema inline all'interno dell'origine XML. Il valore predefinito di questa proprietà è **False**.|  
|XMLData|string|File o variabili da cui recuperare i dati XML.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
|XMLSchemaDefinition|string|Percorso e nome del file di definizione dello schema (estensione xsd).<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'output dell'origine XML. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|RowsetID|string|Valore che identifica il set di righe associato all'output.|  
  
 Le colonne di output dell'origine XML non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Origine XML](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
