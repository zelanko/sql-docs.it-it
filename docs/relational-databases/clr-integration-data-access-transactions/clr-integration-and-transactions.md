---
title: Integrazione e transazioni CLR | Microsoft Docs
description: Lo spazio dei nomi System. Transactions fornisce un Framework di transazione completamente integrato con ADO.NET e SQL Server l'integrazione con CLR.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c93aec2d5246073073fefaaaf4b21d3d542416a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737661"
---
# <a name="clr-integration-and-transactions"></a>Integrazione con CLR e transazioni
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Lo spazio dei nomi **System. Transactions** fornisce un Framework di transazione completamente integrato con ADO.NET e l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrazione con Common Language Runtime (CLR). **System. Transactions** e ADO.NET collaborano per estendere e semplificare l'utilizzo di transazioni locali e distribuite nelle applicazioni gestite.  
  
> [!NOTE]  
>  Una procedura CLR definita dall'utente non può stabilire una connessione allo stesso server nel quale viene eseguita, ovvero una connessione loopback, ed essere integrata nella stessa transazione. Un eventuale tentativo di connessione verrà bloccato e il controllo non verrà restituito alla procedura definita dall'utente. Verrà pertanto generato un errore di timeout (messaggio 1206) nella procedura definita dall'utente.  
  
 Per ulteriori informazioni sulle transazioni e su .NET Framework, vedere gli argomenti relativi all'esecuzione e all'utilizzo di transazioni in .NET Framework SDK.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Promozione delle transazioni](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 Viene illustrata la possibilità di promuovere le transazioni e viene spiegato come utilizzare tale caratteristica.  
  
 [Accesso alla transazione corrente](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 Viene illustrato come accedere a una transazione attualmente in esecuzione in-process in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Utilizzo di System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 Viene descritto come usare l'Application Programming Interface **System. Transactions** (API) nell'applicazione gestita.  
  
 [Durata delle transazioni](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 Viene illustrata la differenza in termini di durata tra le transazioni avviate in stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] e quelle avviate in applicazioni CLR.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso ai dati da oggetti di database CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
