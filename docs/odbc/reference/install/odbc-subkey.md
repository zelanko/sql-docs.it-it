---
title: Sottochiave ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aad5171b98c54aa0c4adbde1a5678e4fd953640
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093958"
---
# <a name="odbc-subkey"></a>Sottochiave ODBC
I valori nella sottochiave ODBC specificano le opzioni di traccia ODBC. Queste opzioni vengono impostate tramite la scheda di traccia della finestra di dialogo Amministrazione origine dati ODBC visualizzato dal **SQLManageDataSources**. Sottochiave ODBC stesso è facoltativa. Il formato di questi valori è come illustrato nella tabella seguente.  
  
|NOME|Tipo di dati|Data|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 I valori hanno i significati descritti nella tabella seguente.  
  
|Value|Significato|  
|-----------|-------------|  
|Trace|Se il valore di traccia è impostato su 1 quando un'applicazione chiama **SQLAllocHandle** con l'opzione SQL_HANDLE_ENV, traccia è abilitata per l'applicazione chiamante.<br /><br /> Se la parola chiave traccia è impostata su 0 quando un'applicazione chiama **SQLAllocHandle** con l'opzione SQL_HANDLE_ENV, la traccia è disabilitata per l'applicazione chiamante. Rappresenta il valore predefinito.<br /><br /> Un'applicazione può abilitare o disabilitare la traccia con l'attributo di connessione SQL_ATTR_TRACE. Tuttavia, tale operazione non modifica i dati per questo valore.|  
|TraceFile|Se la traccia è abilitata, gestione Driver scrive nel file di traccia specificato dal valore TraceFile.<br /><br /> Se viene specificato alcun file di traccia, gestione Driver scrive il file SQL. log nell'unità corrente. Rappresenta il valore predefinito.<br /><br /> Traccia deve essere usata solo per una singola applicazione oppure ogni applicazione deve specificare un file di traccia diversi. In caso contrario, due o più applicazioni tenterà di aprire lo stesso file di traccia allo stesso tempo, causando un errore.<br /><br /> Un'applicazione può specificare un nuovo file di traccia con l'attributo di connessione SQL_ATTR_TRACEFILE. Tuttavia, tale operazione non modifica i dati per questo valore.|  
  
 Ad esempio, si supponga che la traccia è abilitata e il file di traccia C:\Odbc.log. I valori nella sottochiave ODBC sarà come segue:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
