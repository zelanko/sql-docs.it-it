---
title: Proprietà personalizzate del file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d98592143f3f13313e5b281dc689abbe44ddbb1f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749685"
---
# <a name="flat-file-custom-properties"></a>Proprietà personalizzate del file flat
  **Proprietà personalizzate delle origini**  
  
 L'origine file flat include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine file flat. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|Nome di una colonna di output contenente il nome file. Se non si specifica alcun nome, non verrà generata alcuna colonna contenente il nome file.<br /><br /> Nota: Questa proprietà non è disponibile nel **Editor origine File Flat**, ma può essere impostata tramite il **Editor avanzato**.|  
|RetainNulls|Boolean|Valore che specifica se i valori Null dal file di origine devono essere mantenuti come tali durante l'elaborazione dei dati tramite il motore della pipeline di trasformazione dati. Il valore predefinito di questa proprietà è `False`.|  
  
 L'output dell'origine file flat non include proprietà personalizzate.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output dell'origine file flat. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|Valore che indica se la colonna utilizza le routine di analisi più veloci ma indipendenti dalle impostazioni locali disponibili in DTS oppure le routine di analisi standard dipendenti dalle impostazioni locali. Per altre informazioni, vedere [Analisi veloce](../fast-parse.md) e [Analisi standard](../standard-parse.md). Il valore predefinito di questa proprietà è `False`.<br /><br /> Nota: Questa proprietà non è disponibile nel **Editor origine File Flat**, ma può essere impostata tramite il **Editor avanzato**.|  
  
 Per altre informazioni, vedere [Origine file flat](flat-file-source.md).  
  
 **Proprietà personalizzate delle destinazioni**  
  
 La destinazione file flat include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione file flat. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|Intestazione|String|Blocco di testo inserito nel file prima di iniziare a scrivere i dati.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
|Overwrite|Boolean|Valore che specifica se sovrascrivere o aggiungere dati a un file di destinazione esistente con lo stesso nome. Il valore predefinito di questa proprietà è `True`.|  
  
 L'input e le colonne di input della destinazione file flat non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione file flat](flat-file-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
