---
title: Rappresentazione e sicurezza dell'integrazione con CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2c32691a065c2bfc43868d6b4105fbf1395a63ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781129"
---
# <a name="impersonation-and-clr-integration-security"></a>Rappresentazione e sicurezza per l'integrazione con CLR
  Quando il codice gestito accede alle risorse esterne, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non rappresenta automaticamente il contesto di esecuzione corrente nel quale viene eseguita la routine. Il contesto di esecuzione corrente può essere rappresentato in modo esplicito dal codice degli assembly `EXTERNAL_ACCESS` e `UNSAFE`.  
  
> [!NOTE]  
>  Per informazioni sulle modifiche del comportamento nella rappresentazione, vedere [modifiche di rilievo apportate alle funzionalità di motore di database in SQL Server 2014](../breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Il provider di accesso ai dati in-process fornisce un'API, `SqlContext.WindowsIdentity`, che può essere utilizzata per recuperare il token associato al contesto di sicurezza corrente. Il codice gestito degli assembly `EXTERNAL_ACCESS` e `UNSAFE` può utilizzare questo metodo per recuperare il contesto e servirsi del metodo .NET Framework `WindowsIdentity.Impersonate` per rappresentarlo. Di seguito sono indicate le restrizioni che si applicano quando il codice utente esegue una rappresentazione in modo esplicito:  
  
-   L'accesso ai dati in-process non è consentito quando il codice gestito si trova in uno stato rappresentato. Il codice può annullare la rappresentazione, quindi chiamare l'accesso ai dati in-process. Si noti che questa operazione richiede l'archiviazione del valore restituito (un oggetto `WindowsImpersonationContext`) del metodo `Impersonate` originale e la chiamata al metodo `Undo` su questo oggetto `WindowsImpersonationContext`.  
  
     Come conseguenza di questa restrizione, durante l'accesso ai dati in-process, questo si verifica sempre nel contesto di sicurezza corrente attivo per la sessione e non può essere modificato dalla rappresentazione esplicita all'interno del codice gestito.  
  
-   Per il codice gestito che viene eseguito in modo asincrono (ad esempio tramite gli assembly `UNSAFE` che creano thread ed eseguono il codice in modo asincrono), l'accesso ai dati in-process non è mai consentito. Ciò accade indipendentemente dalla rappresentazione.  
  
 Quando il codice è in esecuzione in un contesto rappresentato diverso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], non può eseguire le chiamate di accesso ai dati in-process. Prima di effettuare chiamate di accesso ai dati in-process, è necessario annullare il contesto di rappresentazione. Quando l'accesso ai dati in-process viene effettuato da codice gestito, per l'autorizzazione viene utilizzato sempre il contesto di esecuzione originale del punto di ingresso [!INCLUDE[tsql](../../includes/tsql-md.md)] nel codice gestito.  
  
 Gli assembly `EXTERNAL_ACCESS` e `UNSAFE` accedono alle risorse del sistema operativo con l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a meno che non rappresentino volontariamente il contesto di sicurezza corrente come descritto in precedenza. Per questo motivo, gli autori degli assembly `EXTERNAL_ACCESS` richiedono un livello di attendibilità superiore rispetto a quello degli assembly `SAFE`, specificato dall'autorizzazione a livello di accesso `EXTERNAL ACCESS`. L'autorizzazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dovrebbe, pertanto, essere concessa solo agli accessi attendibili per l'esecuzione del codice nell'account del servizio `EXTERNAL ACCESS`.  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dell'integrazione con CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Rappresentazione e credenziali per le connessioni](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
