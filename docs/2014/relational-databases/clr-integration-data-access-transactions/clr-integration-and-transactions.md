---
title: Integrazione e transazioni CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: de72a2113aeb568decbdc9b5ee0174160cc0d3ef
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955056"
---
# <a name="clr-integration-and-transactions"></a>Integrazione con CLR e transazioni
  Tramite lo spazio dei nomi `System.Transactions` vengono forniti un framework di transazioni pienamente integrato con ADO.NET e l'integrazione con CRL di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `System.Transactions` e ADO.NET funzionano insieme per estendere e semplificare l'utilizzo di transazioni locali e distribuite nelle applicazioni gestite.  
  
> [!NOTE]  
>  Una procedura CLR definita dall'utente non può stabilire una connessione allo stesso server nel quale viene eseguita, ovvero una connessione loopback, ed essere integrata nella stessa transazione. Un eventuale tentativo di connessione verrà bloccato e il controllo non verrà restituito alla procedura definita dall'utente. Verrà pertanto generato un errore di timeout (messaggio 1206) nella procedura definita dall'utente.  
  
 Per ulteriori informazioni sulle transazioni e su .NET Framework, vedere gli argomenti relativi all'esecuzione e all'utilizzo di transazioni in .NET Framework SDK.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Promozione delle transazioni](transaction-promotion.md)  
 Viene illustrata la possibilità di promuovere le transazioni e viene spiegato come utilizzare tale caratteristica.  
  
 [Accesso alla transazione corrente](accessing-the-current-transaction.md)  
 Viene illustrato come accedere a una transazione attualmente in esecuzione in-process in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Utilizzo di System.Transactions](../native-client-ole-db-transactions/transactions.md)  
 Viene illustrato come utilizzare l'API `System.Transactions` nell'applicazione gestita.  
  
 [Durata delle transazioni](transaction-lifetimes.md)  
 Viene illustrata la differenza in termini di durata tra le transazioni avviate in stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] e quelle avviate in applicazioni CLR.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso ai dati da oggetti di database CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
