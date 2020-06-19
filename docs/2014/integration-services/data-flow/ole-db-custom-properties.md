---
title: Proprietà personalizzate OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0e40db8f1441da112cd5e2bd1a77d10323b5891c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914951"
---
# <a name="ole-db-custom-properties"></a>Proprietà personalizzate OLE DB
  **Proprietà personalizzate delle origini**  
  
 L'origine OLE DB include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine OLE DB. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modalità utilizzata per accedere al database. I valori possibili sono **Apri set di righe**, **Apri set di righe da variabile**, `SQL Command` e **comando SQL da variabile**. Il valore predefinito è **OpenRowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Valore che indica se utilizzare il valore della proprietà `DefaultCodePage` per ogni colonna o se tentare di dedurre la tabella codici dalle impostazioni locali di ogni colonna. Il valore predefinito di questa proprietà è `False`.|  
|CommandTimeout|Integer|Numero di secondi prima del timeout del comando. Il valore 0 indica un timeout infinito.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor origine OLE DB**, ma può essere impostata tramite **Editor avanzato**.|  
|DefaultCodePage|Integer|Tabella codici da utilizzare quando le informazioni sulla tabella codici non sono disponibili dall'origine dati.|  
|OpenRowset|string|Nome dell'oggetto di database utilizzato per aprire un set di righe.|  
|OpenRowsetVariable|string|Variabile che contiene il nome dell'oggetto di database utilizzato per aprire un set di righe.|  
|ParameterMapping|string|Mapping tra i parametri nel comando SQL e le variabili.|  
|SqlCommand|string|Comando SQL da eseguire.|  
|SqlCommandVariable|string|Variabile che contiene il comando SQL da eseguire.|  
  
 L'output e le colonne di output dell'origine OLE DB non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [OLE DB Source](ole-db-source.md).  
  
 **Proprietà personalizzate delle destinazioni**  
  
 La destinazione OLE DB include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione OLE DB. Tutte le proprietà sono di lettura/scrittura.  
  
> [!NOTE]  
>  Le opzioni FastLoad elencate nella tabella (FastLoadKeepIdentity, FastLoadKeepNulls e FastLoadOptions) corrispondono alle proprietà con nome simile esposte dall'interfaccia `IRowsetFastLoad` implementata dal provider Microsoft OLE DB per SQL Server (SQLOLEDB). Per ulteriori informazioni, eseguire una ricerca di IRowsetFastLoad nel sito Web MSDN Library.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumerazione)|Valore che specifica la modalità di accesso della destinazione al relativo database di destinazione.<br /><br /> Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> `OpenRowset`(0): specificare il nome di una tabella o di una vista.<br />`OpenRowset from Variable`(1): specificare il nome di una variabile che contiene il nome di una tabella o di una vista.<br />`OpenRowset Using Fastload`(3): specificare il nome di una tabella o di una vista.<br />`OpenRowset Using Fastload from Variable`(4): specificare il nome di una variabile che contiene il nome di una tabella o di una vista.<br />`SQL Command`(2): viene fornita un'istruzione SQL.|  
|AlwaysUseDefaultCodePage|Boolean|Valore che indica se utilizzare il valore della proprietà `DefaultCodePage` per ogni colonna o se tentare di dedurre la tabella codici dalle impostazioni locali di ogni colonna. Il valore predefinito di questa proprietà è `False`.|  
|CommandTimeout|Integer|Numero massimo di secondi durante i quali è possibile eseguire il comando SQL prima del timeout. Il valore 0 corrisponde a un intervallo infinito. Il valore predefinito di questa proprietà è 0.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor destinazione OLE DB**, ma può essere impostata tramite **Editor avanzato**.|  
|DefaultCodePage|Integer|Tabella codici predefinita associata alla destinazione OLE DB.|  
|FastLoadKeepIdentity|Boolean|Valore che specifica se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo con una delle opzioni di caricamento rapido. Il valore predefinito di questa proprietà è `False`. Questa proprietà corrisponde alla proprietà OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) `SSPROP_FASTLOADKEEPIDENTITY` .|  
|FastLoadKeepNulls|Boolean|Valore che specifica se copiare i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con una delle opzioni di caricamento rapido. Il valore predefinito di questa proprietà è `False`. Questa proprietà corrisponde alla proprietà OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) `SSPROP_FASTLOADKEEPNULLS` .|  
|FastLoadMaxInsertCommitSize|Integer|Valore che specifica le dimensioni del batch di cui la destinazione OLE DB tenta di eseguire il commit durante le operazioni di caricamento rapido. Il valore predefinito **0**indica una singola operazione di commit in seguito all'elaborazione di tutte le righe.|  
|FastLoadOptions|string|Raccolta di opzioni di caricamento rapido. Tra le opzioni di caricamento rapido sono inclusi il blocco delle tabelle e la verifica dei vincoli. È possibile specificare una, nessuna o entrambe le opzioni. Questa proprietà corrisponde alla proprietà OLE DB IRowsetFastLoad `SSPROP_FASTLOADOPTIONS` e accetta opzioni di stringa, ad esempio `CHECK_CONSTRAINTS` e `TABLOCK` .<br /><br /> Nota: Alcune opzioni valide per questa proprietà non sono disponibili in **Editor destinazione Excel**, ma possono essere impostate tramite **Editor avanzato**.|  
|OpenRowset|string|Quando AccessMode è `OpenRowset` , il nome della tabella o della vista a cui accede la OLE DB di destinazione.|  
|OpenRowsetVariable|string|Quando AccessMode è `OpenRowset from Variable` , il nome della variabile che contiene il nome della tabella o della vista a cui accede la OLE DB destinazione.|  
|SqlCommand|string|Quando AccessMode è `SQL Command` , istruzione Transact-SQL utilizzata dalla destinazione OLE DB per specificare le colonne di destinazione per i dati.|  
  
 L'input e le colonne di input della destinazione OLE DB non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [OLE DB Destination](ole-db-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
