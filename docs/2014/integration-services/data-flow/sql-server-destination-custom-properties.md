---
title: Proprietà personalizzate della destinazione SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b736aa6d-c154-44a0-be08-f25733fca1d9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6152a2a06a6814a5e31fd744e9080b0ef53d536c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790833"
---
# <a name="sql-server-destination-custom-properties"></a>Proprietà personalizzate della destinazione SQL Server
  La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include sia proprietà personalizzate sia le proprietà comuni a tutti i componenti del flusso di dati.  
  
 La tabella seguente descrive le proprietà personalizzate della destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AlwaysUseDefaultCodePage|Boolean|Forza l'uso del valore della proprietà DefaultCodePage. Il valore predefinito di questa proprietà è `False`.|  
|BulkInsertCheckConstraints|Boolean|Valore che specifica se l'inserimento bulk verifica i vincoli. Il valore predefinito di questa proprietà è `True`.|  
|BulkInsertFireTriggers|Boolean|Valore che specifica se l'inserimento bulk attiva trigger nelle tabelle. Il valore predefinito di questa proprietà è `False`.|  
|BulkInsertFirstRow|Integer|Valore che specifica la prima riga da inserire. Il valore predefinito di questa proprietà è **-1**, che indica che non è stato assegnato alcun valore.|  
|BulkInsertKeepIdentity|Boolean|Valore che specifica se i valori possono essere inseriti in colonne Identity. Il valore predefinito di questa proprietà è `False`.|  
|BulkInsertKeepNulls|Boolean|Valore che specifica se l'inserimento bulk mantiene i valori Null. Il valore predefinito di questa proprietà è `False`.|  
|BulkInsertLastRow|Integer|Valore che specifica l'ultima riga da inserire. Il valore predefinito di questa proprietà è **-1**, che indica che non è stato assegnato alcun valore.|  
|BulkInsertMaxErrors|Integer|Valore che specifica il numero massimo di errori che possono verificarsi prima dell'arresto dell'inserimento bulk. Il valore predefinito di questa proprietà è **-1**, che indica che non è stato assegnato alcun valore.|  
|BulkInsertOrder|String|Nomi delle colonne di ordinamento. È possibile ordinare ogni colonna in ordine crescente o decrescente. Se si utilizzano più colonne di ordinamento, i nomi delle colonne saranno separati da virgole.|  
|BulkInsertTableName|String|Tabella o vista [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database in cui vengono copiati i dati.|  
|BulkInsertTablock|Boolean|Valore che specifica se la tabella è bloccata durante l'inserimento bulk. Il valore predefinito di questa proprietà è `True`.|  
|DefaultCodePage|Integer|Tabella codici da utilizzare quando le informazioni sulla tabella codici non sono disponibili dall'origine dati.|  
|MaxInsertCommitSize|Integer|Valore che specifica il numero massimo di righe da inserire in un batch. Quando il valore è zero, tutte le righe vengono inserite in un singolo batch.|  
|Timeout|Integer|Valore che specifica il numero di secondi di attesa della destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima della chiusura se non vi sono dati disponibili per l'inserimento. Il valore 0 indica l'assenza di timeout per la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il valore predefinito di questa proprietà è 30.|  
  
 L'input e le colonne di input della destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione SQL Server](sql-server-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
