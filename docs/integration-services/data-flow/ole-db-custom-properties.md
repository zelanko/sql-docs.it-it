---
title: Proprietà personalizzate OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 039b36c2092d9e08e81802e441f42587be66445c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298154"
---
# <a name="ole-db-custom-properties"></a>Proprietà personalizzate OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Proprietà personalizzate delle origini**  
  
 L'origine OLE DB include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine OLE DB. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modalità utilizzata per accedere al database. I valori possibili sono **OpenRowset**, **OpenRowset da variabile**, **Comando SQL**e **Comando SQL da variabile**. Il valore predefinito è **OpenRowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Valore che indica se utilizzare il valore della proprietà **DefaultCodePage** per ogni colonna o se tentare di dedurre la tabella codici dalle impostazioni locali di ogni colonna. Il valore predefinito di questa proprietà è **False**.|  
|CommandTimeout|Integer|Numero di secondi prima del timeout del comando. Il valore 0 indica un timeout infinito.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor origine OLE DB**, ma può essere impostata tramite **Editor avanzato**.|  
|DefaultCodePage|Integer|Tabella codici da utilizzare quando le informazioni sulla tabella codici non sono disponibili dall'origine dati.|  
|OpenRowset|string|Nome dell'oggetto di database utilizzato per aprire un set di righe.|  
|OpenRowsetVariable|string|Variabile che contiene il nome dell'oggetto di database utilizzato per aprire un set di righe.|  
|ParameterMapping|string|Mapping tra i parametri nel comando SQL e le variabili.|  
|SqlCommand|string|Comando SQL da eseguire.|  
|SqlCommandVariable|string|Variabile che contiene il comando SQL da eseguire.|  
  
 L'output e le colonne di output dell'origine OLE DB non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
 **Proprietà personalizzate delle destinazioni**  
  
 La destinazione OLE DB include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione OLE DB. Tutte le proprietà sono di lettura/scrittura.  
  
> [!NOTE]  
>  Le opzioni FastLoad elencate nella tabella (FastLoadKeepIdentity, FastLoadKeepNulls e FastLoadOptions) corrispondono alle proprietà con nome simile esposte dall'interfaccia **IRowsetFastLoad** implementata dal provider Microsoft OLE DB per SQL Server (SQLOLEDB). Per ulteriori informazioni, eseguire una ricerca di IRowsetFastLoad nel sito Web MSDN Library.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumerazione)|Valore che specifica la modalità di accesso della destinazione al relativo database di destinazione.<br /><br /> Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> <br /><br /> **OpenRowset** (0): specificare il nome di una tabella o di una vista.<br /><br /> **OpenRowset da variabile** (1): specificare il nome di una variabile contenente il nome di una tabella o di una vista.<br /><br /> **OpenRowset con Fastload** (3): specificare il nome di una tabella o di una vista.<br /><br /> **OpenRowset con Fastload da variabile** (4): specificare il nome di una variabile contenente il nome di una tabella o di una vista.<br /><br /> **Comando SQL** (2): specificare un'istruzione SQL.|  
|AlwaysUseDefaultCodePage|Boolean|Valore che indica se utilizzare il valore della proprietà **DefaultCodePage** per ogni colonna o se tentare di dedurre la tabella codici dalle impostazioni locali di ogni colonna. Il valore predefinito di questa proprietà è **False**.|  
|CommandTimeout|Integer|Numero massimo di secondi durante i quali è possibile eseguire il comando SQL prima del timeout. Il valore 0 corrisponde a un intervallo infinito. Il valore predefinito di questa proprietà è 0.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor destinazione OLE DB**, ma può essere impostata tramite **Editor avanzato**.|  
|DefaultCodePage|Integer|Tabella codici predefinita associata alla destinazione OLE DB.|  
|FastLoadKeepIdentity|Boolean|Valore che specifica se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo con una delle opzioni di caricamento rapido. Il valore predefinito di questa proprietà è **False**. Questa proprietà corrisponde alla proprietà OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)**SSPROP_FASTLOADKEEPIDENTITY**.|  
|FastLoadKeepNulls|Boolean|Valore che specifica se copiare i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con una delle opzioni di caricamento rapido. Il valore predefinito di questa proprietà è **False**. Questa proprietà corrisponde alla proprietà OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)**SSPROP_FASTLOADKEEPNULLS**.|  
|FastLoadMaxInsertCommitSize|Integer|Valore che specifica le dimensioni del batch di cui la destinazione OLE DB tenta di eseguire il commit durante le operazioni di caricamento rapido. Il valore predefinito **0**indica una singola operazione di commit in seguito all'elaborazione di tutte le righe.|  
|FastLoadOptions|string|Raccolta di opzioni di caricamento rapido. Tra le opzioni di caricamento rapido sono inclusi il blocco delle tabelle e la verifica dei vincoli. È possibile specificare una, nessuna o entrambe le opzioni. Questa proprietà corrisponde alla proprietà OLE DB IRowsetFastLoad **SSPROP_FASTLOADOPTIONS** e accetta opzioni stringa, ad esempio **CHECK_CONSTRAINTS** e **TABLOCK**.<br /><br /> Nota: Alcune opzioni valide per questa proprietà non sono disponibili in **Editor destinazione Excel**, ma possono essere impostate tramite **Editor avanzato**.|  
|OpenRowset|string|Quando AccessMode è **OpenRowset**, nome della tabella o della vista a cui accede la destinazione OLE DB.|  
|OpenRowsetVariable|string|Quando AccessMode è **OpenRowset da variabile**, nome della variabile che contiene il nome della tabella o della vista a cui accede la destinazione OLE DB.|  
|SqlCommand|string|Quando AccessMode è **Comando SQL**, istruzione Transact-SQL usata dalla destinazione OLE DB per specificare le colonne di destinazione per i dati.|  
  
 L'input e le colonne di input della destinazione OLE DB non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
