---
title: 'Sottochiave ODBC : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96e9a5f4c3cdac5097686528d3c089d9ec5826f7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287441"
---
# <a name="odbc-subkey"></a>Sottochiave ODBC
I valori nella sottochiave ODBC specificano le opzioni di traccia ODBC. Queste opzioni vengono impostate tramite la scheda Traccia della finestra di dialogo Amministratore origine dati ODBC visualizzata da **SQLManageDataSources**. La sottochiave ODBC stessa è facoltativa. Il formato di questi valori è come illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*percorso del file di traccia*|  
  
 I valori hanno i significati descritti nella tabella seguente.  
  
|Valore|Significato|  
|-----------|-------------|  
|Trace|Se il valore Trace è impostato su 1 quando un'applicazione chiama **SQLAllocHandle** con l'opzione SQL_HANDLE_ENV, la traccia è abilitata per l'applicazione chiamante.<br /><br /> Se la parola chiave Trace è impostata su 0 quando un'applicazione chiama **SQLAllocHandle** con l'opzione SQL_HANDLE_ENV, la traccia è disabilitata per l'applicazione chiamante. Si tratta del valore predefinito.<br /><br /> Un'applicazione può abilitare o disabilitare la traccia con l'attributo di connessione SQL_ATTR_TRACE. Tuttavia, questa operazione non modifica i dati per questo valore.|  
|TraceFile|Se la tracciatura è abilitata, Gestione Driver scrive nel file di traccia specificato dal TraceFile valore.<br /><br /> Se non viene specificato alcun file di traccia, Gestione Driver scrive nel file Sql.log nell'unità corrente. Si tratta del valore predefinito.<br /><br /> La traccia deve essere utilizzata solo per una singola applicazione oppure ogni applicazione deve specificare un file di traccia diverso. In caso contrario, due o più applicazioni tenteranno di aprire lo stesso file di traccia contemporaneamente, causando un errore.<br /><br /> Un'applicazione può specificare un nuovo file di traccia con l'attributo di connessione SQL_ATTR_TRACEFILE. Tuttavia, questa operazione non modifica i dati per questo valore.|  
  
 Si supponga, ad esempio, che la traccia sia abilitata e che il file di traccia sia C:. I valori nella sottochiave ODBC sono i seguenti:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
