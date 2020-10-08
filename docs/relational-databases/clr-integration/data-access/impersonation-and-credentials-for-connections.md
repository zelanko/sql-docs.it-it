---
title: Rappresentazione e credenziali per le connessioni | Microsoft Docs
description: In SQL Server integrazione con CLR, è possibile rappresentare il chiamante nell'autenticazione di Windows utilizzando la proprietà SqlContext. WindowsIdentity.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
author: rothja
ms.author: jroth
ms.openlocfilehash: a6487b61d9c21ee86acad28413fb8a0439731b33
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810838"
---
# <a name="impersonation-and-credentials-for-connections"></a>Rappresentazione e credenziali per le connessioni
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Nell'integrazione con Common Language Runtime (CRL) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'utilizzo dell'autenticazione di Windows è complesso, ma più sicuro rispetto all'autenticazione di SQL Server. Utilizzando l'autenticazione di Windows, è necessario tenere conto di alcune considerazioni.  
  
 Per impostazione predefinita, un processo di SQL Server che si connette a Windows acquisisce il contesto di sicurezza dell'account di servizio Windows di SQL Server. È tuttavia possibile eseguire il mapping di una funzione CLR a un'identità del proxy, in modo che le connessioni in uscita dispongano di un contesto di sicurezza diverso da quello dell'account di servizio Windows.  
  
 In alcuni casi, potrebbe essere necessario rappresentare il chiamante utilizzando la proprietà **SqlContext. WindowsIdentity** anziché eseguire come account del servizio. L'istanza **WindowsIdentity** rappresenta l'identità del client che ha richiamato il codice chiamante ed è disponibile solo quando il client usa l'autenticazione di Windows. Una volta ottenuta l'istanza di **WindowsIdentity** , è possibile chiamare **Impersonate** per modificare il token di sicurezza del thread, quindi aprire connessioni ADO.NET per conto del client.  
  
 Dopo aver chiamato SqlContext. WindowsIdentity. Impersonate, non è possibile accedere ai dati locali e non è possibile accedere ai dati di sistema. Per accedere di nuovo ai dati, è necessario chiamare WindowsImpersonationContext. Undo.  
  
 Nell'esempio seguente viene illustrato come rappresentare il chiamante utilizzando la proprietà **SqlContext. WindowsIdentity** .  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  Per informazioni sulle modifiche del comportamento nella rappresentazione, vedere [modifiche di rilievo apportate alle funzionalità di motore di database in SQL Server 2016](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Inoltre, se è stata ottenuta l'istanza dell'identità di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, per impostazione predefinita non è possibile propagarla in un altro computer, in quanto la propagazione è limitata dall'infrastruttura di sicurezza di Windows. Esiste tuttavia un meccanismo noto come "delega" che abilita la propagazione delle identità di Windows in più computer attendibili. Per ulteriori informazioni sulla delega, vedere l'articolo TechNet "[transizione del protocollo Kerberos e delega vincolata](/previous-versions/windows/it-pro/windows-server-2003/cc739587(v=ws.10))".  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto SqlContext](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
