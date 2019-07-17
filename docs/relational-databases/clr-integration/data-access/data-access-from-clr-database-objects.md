---
title: Accesso ai dati da oggetti di Database CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
ms.openlocfilehash: 29110ecb83493ec95fbc594d0f743c3c4cb07a68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216405"
---
# <a name="data-access-from-clr-database-objects"></a>Accesso ai dati da oggetti di database CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una routine di common language runtime (CLR) possa accedere facilmente a dati archiviati nell'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui è in esecuzione, nonché ai dati archiviati in istanze remote. I dati specifici cui può accedere la routine sono determinati dal contesto utente in cui viene eseguito il codice. Accedere ai dati da un oggetto di database CLR utilizzando il Provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], anche detta **SqlClient**. Si tratta dello stesso provider utilizzato dagli sviluppatori che accedono a dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da applicazioni client e di livello intermedio gestite. Per questo motivo, è possibile sfruttare le proprie conoscenze di ADO.NET e **SqlClient** nelle applicazioni client e il livello intermedio.  
  
> [!NOTE]  
>  Per impostazione predefinita, ai metodi con tipo definito dall'utente e alle funzioni definite dall'utente non è consentito eseguire accesso ai dati. È necessario impostare il **DataAccess** proprietà di **SqlMethodAttribute** oppure **SqlFunctionAttribute** al **DataAccessKind. Read** per abilitare accesso ai dati di sola lettura da metodi con tipo definito dall'utente (UDT) o funzioni definite dall'utente. Le operazioni di modifica dei dati non sono consentite da tipi definiti dall'utente o funzioni definite dall'utente e, in caso di un tentativo a tale scopo, vengono generate eccezioni in fase di esecuzione.  
  
 In questa sezione vengono illustrate solo le specifiche differenze funzionali e di comportamento durante l'accesso ai dati da un oggetto di database CLR. Per ulteriori informazioni su caratteristiche e funzionalità di ADO.NET, vedere la documentazione di ADO.NET inclusa in .NET Framework SDK.  
  
 Nella tabella seguente vengono elencati gli argomenti disponibili in questa sezione.  
  
 [Connessione di contesto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
 Viene descritta la connessione di contesto a SQL Server.  
  
 [Rappresentazione e credenziali per le connessioni](../../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
 Viene descritta la rappresentazione di connessioni e credenziali di connessione.  
  
 [Estensioni specifiche In-Process di SQL Server ad ADO.NET](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 Vengono illustrate le specifiche in-process **SqlPipe**, **SqlContext**, **SqlTriggerContext**, e **SqlDataRecord** oggetti.  
  
 [Integrazione con CLR e transazioni](../../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
 Viene descritta l'integrazione del nuovo framework di transazioni fornito nello spazio dei nomi System.Transactions con ADO.NET e l'integrazione CLR di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Serializzazione XML da oggetti di database CLR](https://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344)  
 Viene illustrato come consentire scenari di serializzazione XML di oggetti di database CLR all'interno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
