---
title: Proprietà personalizzate di Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8d556a199b608659a9ceaaeb3b7036155886d6c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827234"
---
# <a name="excel-custom-properties"></a>Proprietà personalizzate di Excel
  **Proprietà personalizzate delle origini**  
  
 L'origine Excel include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine Excel. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modalità utilizzata per accedere al database. I valori possibili sono **Apri set di righe**, **Apri set di righe da variabile**, `SQL Command`e **comando SQL da variabile**. Il valore predefinito è **OpenRowset**.|  
|CommandTimeout|Integer|Numero di secondi prima del timeout del comando.  Il valore 0 indica un timeout infinito.<br /><br /> **Nota** Questa proprietà non è disponibile in **Editor origine Excel**, ma può essere impostata tramite **Editor avanzato**.|  
|OpenRowset|string|Nome dell'oggetto di database utilizzato per aprire un set di righe.|  
|OpenRowsetVariable|string|Variabile che contiene il nome dell'oggetto di database utilizzato per aprire un set di righe.|  
|ParameterMapping|string|Mapping tra i parametri nel comando SQL e le variabili.|  
|SqlCommand|string|Comando SQL da eseguire.|  
|SqlCommandVariable|string|Variabile che contiene il comando SQL da eseguire.|  
  
 L'output e le colonne di output dell'origine Excel non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Origine Excel](excel-source.md).  
  
 **Proprietà personalizzate delle destinazioni**  
  
 La destinazione Excel include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione Excel. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumerazione)|Valore che specifica la modalità di accesso della destinazione al relativo database di destinazione.<br /><br /> Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> `OpenRowset`(0): viene fornito il nome di una tabella o di una vista.<br /><br /> `OpenRowset from Variable`(1): viene fornito il nome di una variabile che contiene il nome di una tabella o di una vista.<br /><br /> `OpenRowset Using Fastload`(3): specificare il nome di una tabella o di una vista.<br /><br /> `OpenRowset Using Fastload from Variable`(4): specificare il nome di una variabile che contiene il nome di una tabella o di una vista.<br /><br /> `SQL Command`(2): viene fornita un'istruzione SQL.|  
|CommandTimeout|Integer|Numero massimo di secondi durante i quali è possibile eseguire il comando SQL prima del timeout. Il valore **0** corrisponde a un intervallo infinito. Il valore predefinito di questa proprietà è **0**.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor destinazione Excel**, ma può essere impostata tramite **Editor avanzato**.|  
|FastLoadKeepIdentity|Boolean|Valore che specifica se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo quando si utilizza una delle opzioni di caricamento rapido. Il valore predefinito di questa proprietà è **False**.|  
|FastLoadKeepNulls|Boolean|Valore che specifica se copiare i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con una delle opzioni di caricamento rapido. Il valore predefinito di questa proprietà è **False**.|  
|FastLoadMaxInsertCommitSize|Integer|Valore che specifica le dimensioni del batch di cui la destinazione Excel tenta di eseguire il commit durante le operazioni di caricamento rapido. Il valore predefinito è **2147483647**. Il valore **0** indica una singola operazione di commit in seguito all'elaborazione di tutte le righe.|  
|FastLoadOptions|string|Raccolta di opzioni di caricamento rapido. Tra le opzioni di caricamento rapido sono inclusi il blocco delle tabelle e la verifica dei vincoli. È possibile specificare una, nessuna o entrambe le opzioni.<br /><br /> Nota: Alcune opzioni valide per questa proprietà non sono disponibili in **Editor destinazione Excel**, ma possono essere impostate tramite **Editor avanzato**.|  
|OpenRowset|string|Quando AccessMode è `OpenRowset`, il nome della tabella o della vista a cui accede la destinazione Excel.|  
|OpenRowsetVariable|string|Quando AccessMode è `OpenRowset from Variable`, il nome della variabile che contiene il nome della tabella o della vista a cui accede la destinazione Excel.|  
|SqlCommand|string|Quando AccessMode è `SQL Command`, istruzione Transact-SQL utilizzata dalla destinazione Excel per specificare le colonne di destinazione per i dati.|  
  
 L'input e le colonne di input della destinazione Excel non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione Excel](excel-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
