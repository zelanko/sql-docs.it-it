---
description: Sottochiave ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec27b40e196f5277307b9a299dd865a1604dc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499726"
---
# <a name="odbc-subkey"></a>Sottochiave ODBC
I valori nella sottochiave ODBC specificano le opzioni di traccia ODBC. Queste opzioni vengono impostate tramite la scheda traccia della finestra di dialogo Amministrazione origine dati ODBC visualizzata da **SQLManageDataSources**. La sottochiave ODBC è facoltativa. Il formato di questi valori è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*TraceFile-percorso*|  
  
 I valori hanno i significati descritti nella tabella seguente.  
  
|Valore|Significato|  
|-----------|-------------|  
|Trace|Se il valore della traccia è impostato su 1 quando un'applicazione chiama **SQLAllocHandle** con l'opzione SQL_HANDLE_ENV, la traccia è abilitata per l'applicazione chiamante.<br /><br /> Se la parola chiave Trace è impostata su 0 quando un'applicazione chiama **SQLAllocHandle** con l'opzione SQL_HANDLE_ENV, la traccia viene disabilitata per l'applicazione chiamante. Si tratta del valore predefinito.<br /><br /> Un'applicazione può abilitare o disabilitare la traccia con l'attributo di connessione SQL_ATTR_TRACE. Tuttavia, questa operazione non comporta la modifica dei dati per questo valore.|  
|TraceFile|Se la traccia è abilitata, gestione driver scrive nel file di traccia specificato dal valore TraceFile.<br /><br /> Se non viene specificato alcun file di traccia, gestione driver scrive nel file SQL. log nell'unità corrente. Si tratta del valore predefinito.<br /><br /> La traccia deve essere utilizzata solo per una singola applicazione oppure ogni applicazione deve specificare un file di traccia diverso. In caso contrario, due o più applicazioni tenterà di aprire contemporaneamente lo stesso file di traccia, causando un errore.<br /><br /> Un'applicazione può specificare un nuovo file di traccia con l'attributo di connessione SQL_ATTR_TRACEFILE. Tuttavia, questa operazione non comporta la modifica dei dati per questo valore.|  
  
 Si supponga, ad esempio, che la traccia sia abilitata e che il file di traccia sia C:\Odbc.log. I valori nella sottochiave ODBC saranno i seguenti:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
