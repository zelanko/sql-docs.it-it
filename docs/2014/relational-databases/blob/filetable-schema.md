---
title: Schema delle tabelle FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7341919e54a4f669c5251d578ae929f1f4f3e22f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010115"
---
# <a name="filetable-schema"></a>Schema delle tabelle FileTable
  Viene descritto lo schema predefinito e fisso di una tabella FileTable.  
  
|Nome dell'attributo di file|type|Dimensione|Impostazione predefinita|Descrizione|Accessibilità al file system|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|`hierarchyid`|variabile|Oggetto `hierarchyid` che identifica la posizione dell'elemento.|Posizione del nodo corrente nel FileNamespace gerarchico.<br /><br /> Chiave primaria per la tabella.|Può essere creato e modificato impostando i valori del percorso di Windows.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||Valore restituito dalla funzione `NEWID()`.|ID univoco per i dati FILESTREAM.|Non applicabile.|  
|**file_stream**|`varbinary(max)`<br /><br /> `filestream`|variabile|NULL|Contiene i dati FILESTREAM.|Non applicabile.|  
|**file_type**|`nvarchar(255)`|variabile|NULL<br /><br /> Un'operazione di creazione o ridenominazione nel file system popolerà il valore dell'estensione del file in base al nome.|Rappresenta il tipo di file.<br /><br /> Questa colonna può essere utilizzata come `TYPE COLUMN` quando si crea un indice full-text.<br /><br /> **file_type** è una colonna calcolata persistente.|Calcolato automaticamente. Non può essere impostato.|  
|**Name**|`nvarchar(255)`|variabile|Valore GUID.|Nome del file o della directory.|Può essere creato o modificato tramite API di Windows.|  
|**parent_path_locator**|`hierarchyid`|variabile|Oggetto `hierarchyid` che identifica la directory contenente l'elemento.|Valore `hierarchyid` della directory contenitore.<br /><br /> **parent_path_locator** è una colonna calcolata persistente.|Calcolato automaticamente. Non può essere impostato.|  
|**cached_file_size**|`bigint`|||Dimensioni in byte dei dati FILESTREAM.<br /><br /> **cached_file_size** è una colonna calcolata persistente.|Anche se le dimensioni del file memorizzato nella cache vengono aggiornate automaticamente, è possibile che in alcuni casi rari tali dimensioni non siano sincronizzate. Per calcolare le dimensioni esatte, utilizzare la funzione `DATALENGTH()`.|  
|**creation_time**|`datetime2(4)`<br /><br /> `not null`|8 byte|Ora corrente|Data e ora di creazione del file.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**last_write_time**|`datetime2(4)`<br /><br /> `not null`|8 byte|Ora corrente|Data e ora dell'ultimo aggiornamento del file.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**last_access_time**|`datetime2(4)`<br /><br /> `not null`|8 byte|Ora corrente|Data e ora dell'ultimo accesso al file.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**is_directory**|`bit`<br /><br /> `not null`|1 byte|FALSE|Indica se la riga rappresenta una directory. Questo valore viene calcolato in modo implicito e non può essere impostato.|Calcolato automaticamente. Non può essere impostato.|  
|**is_offline**|`bit`<br /><br /> `not null`|1 byte|FALSE|Attributo di file offline.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**is_hidden**|`bit`<br /><br /> `not null`|1 byte|FALSE|Attributo di file nascosto.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**is_readonly**|`bit`<br /><br /> `not null`|1 byte|FALSE|Attributo di file di sola lettura.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**is_archive**|`bit`<br /><br /> `not null`|1 byte|FALSE|Attributo di archivio.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**is_system**|`bit`<br /><br /> `not null`|1 byte|FALSE|Attributo di file di sistema.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
|**is_temporary**|`bit`<br /><br /> `not null`|1 byte|FALSE|Attributo di file temporaneo.|Calcolato automaticamente. Può essere impostato anche tramite API di Windows.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, modificare ed eliminare FileTable](create-alter-and-drop-filetables.md)  
  
  
