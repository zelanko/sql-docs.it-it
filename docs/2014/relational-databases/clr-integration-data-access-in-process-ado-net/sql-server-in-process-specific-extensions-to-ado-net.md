---
title: SQL Server estensioni specifiche in-process per ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
author: rothja
ms.author: jroth
ms.openlocfilehash: 37d8aedc1d8f93739c2e9386665adfc67b43e312
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970789"
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>Estensioni specifiche in-process di SQL Server ad ADO.NET
  Sono disponibili quattro estensioni funzionali principali ad ADO.NET specifiche per l'utilizzo in-process. Tali estensioni verranno analizzate dettagliatamente negli argomenti seguenti.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Oggetto SqlContext](sqlcontext-object.md)  
 Questa classe fornisce accesso alle altre estensioni mediante l'astrazione del contesto di un chiamante di una routine di SQL Server che esegue codice gestito in-process.  
  
 [Oggetto SqlPipe](sqlpipe-object.md)  
 Questa classe contiene routine per l'invio di risultati tabulari e messaggi al client.  
  
 [Oggetto SqlTriggerContext](sqltriggercontext-object.md)  
 Questa classe fornisce informazioni sul contesto nel quale viene eseguito un trigger.  
  
 [Oggetto SqlDataRecord](sqldatarecord-object.md)  
 La classe SqlDataRecord rappresenta una sola riga di dati, insieme ai rispettivi metadati correlati, e consente alle stored procedure di restituire set di risultati personalizzati al client.  
  
  
