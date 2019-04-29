---
title: Rappresentazione e credenziali per le connessioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 50069ad5b96914d98f3d08e795467c2693fabe87
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874016"
---
# <a name="impersonation-and-credentials-for-connections"></a>Rappresentazione e credenziali per le connessioni
  Nell'integrazione con Common Language Runtime (CRL) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'utilizzo dell'autenticazione di Windows è complesso, ma più sicuro rispetto all'autenticazione di SQL Server. Utilizzando l'autenticazione di Windows, è necessario tenere conto di alcune considerazioni.  
  
 Per impostazione predefinita, un processo di SQL Server che si connette a Windows acquisisce il contesto di sicurezza dell'account di servizio Windows di SQL Server. È tuttavia possibile eseguire il mapping di una funzione CLR a un'identità del proxy, in modo che le connessioni in uscita dispongano di un contesto di sicurezza diverso da quello dell'account di servizio Windows.  
  
 In alcuni casi, può essere necessario rappresentare il chiamante tramite la proprietà `SqlContext.WindowsIdentity` anziché procedere con l'esecuzione come account di servizio. L'istanza di `WindowsIdentity` rappresenta l'identità del client che ha richiamato il codice chiamante ed è disponibile solo quando il client ha utilizzato l'autenticazione di Windows. Dopo avere ottenuto l'istanza di `WindowsIdentity`, è possibile chiamare `Impersonate` per modificare il token di sicurezza del thread e quindi aprire le connessioni ADO.NET per conto del client.  
  
 Dopo aver chiamato SQLContext.WindowsIdentity.Impersonate, è possibile accedere ai dati locali e non può accedere ai dati di sistema. Per accedere ai dati anche in questo caso, è necessario chiamare WindowsImpersonationContext.  
  
 Nell'esempio seguente viene illustrata la modalità di rappresentazione del chiamante mediante la proprietà `SqlContext.WindowsIdentity`.  
  
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
>  Per informazioni sulle modifiche del comportamento della rappresentazione, vedere [le modifiche di rilievo alle funzionalità del motore di Database in SQL Server 2014](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Inoltre, se è stata ottenuta l'istanza dell'identità di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, per impostazione predefinita non è possibile propagarla in un altro computer, in quanto la propagazione è limitata dall'infrastruttura di sicurezza di Windows. Esiste tuttavia un meccanismo noto come "delega" che abilita la propagazione delle identità di Windows in più computer attendibili. Altre informazioni sulla delega nell'articolo di TechNet, "[Kerberos Protocol Transition and Constrained Delegation](https://go.microsoft.com/fwlink/?LinkId=50419)".  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto SqlContext](../../clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
