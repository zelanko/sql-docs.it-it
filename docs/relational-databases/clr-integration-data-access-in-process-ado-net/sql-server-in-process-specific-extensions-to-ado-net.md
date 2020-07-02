---
title: SQL Server estensioni in-process a ADO.NET
description: Collegamenti ad articoli sulle quattro principali estensioni funzionali di ADO.NET specifiche per l'utilizzo in-process.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 8265a79c58f94eea59b0776910eda6e4902d5989
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765457"
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>Estensioni specifiche in-process di SQL Server ad ADO.NET
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Sono disponibili quattro estensioni funzionali principali ad ADO.NET specifiche per l'utilizzo in-process. Tali estensioni verranno analizzate dettagliatamente negli argomenti seguenti.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Oggetto SqlContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
 Questa classe fornisce accesso alle altre estensioni mediante l'astrazione del contesto di un chiamante di una routine di SQL Server che esegue codice gestito in-process.  
  
 [Oggetto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
 Questa classe contiene routine per l'invio di risultati tabulari e messaggi al client.  
  
 [Oggetto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)  
 Questa classe fornisce informazioni sul contesto nel quale viene eseguito un trigger.  
  
 [Oggetto SqlDataRecord](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)  
 La classe SqlDataRecord rappresenta una sola riga di dati, insieme ai rispettivi metadati correlati, e consente alle stored procedure di restituire set di risultati personalizzati al client.  
  
  
