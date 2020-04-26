---
title: Aggiunta di una stored procedure estesa a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3a5e5ab2d0dba0d7d39fcf3223f0aeec5ab6a058
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62512349"
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>Aggiunta di una stored procedure estesa a SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 Una DLL che contiene funzioni di stored procedure estese funge da estensione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per installare la DLL, copiare il file in una directory, ad esempio quella che contiene i file dll [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standard (C:\Programmi\Microsoft SQL Server\MSSQL12.0.* x*\MSSQL\Binn per impostazione predefinita).  
  
 Dopo che la DLL della stored procedure estesa è stata copiata nel server, un amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve registrare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ogni funzione di stored procedure estesa presente nella DLL. È possibile eseguire questa operazione utilizzando la stored procedure di sistema sp_addextendedproc.  
  
> [!IMPORTANT]  
>  L'amministratore di sistema deve esaminare con attenzione una stored procedure estesa per assicurarsi che non contenga codice dannoso o malware prima di aggiungerla al server e prima di concedere autorizzazioni di esecuzione ad altri utenti.  Convalidare sempre input di tutti gli utenti. Non concatenare l'input dell'utente prima di convalidarlo. Non eseguire mai un comando creato dall'input dell'utente non convalidato.  
  
 Il primo parametro di sp_addextendedproc specifica il nome della funzione, mentre il secondo specifica il nome della DLL nella quale risiede la funzione. È consigliabile specificare il percorso completo della DLL.  
  
> [!IMPORTANT]  
>  Le DLL esistenti non registrate con un percorso completo non funzionano dopo l'aggiornamento a SQL Server 2005 o versioni successive. Per correggere il problema, utilizzare sp_dropextendedproc per annullare la registrazione della DLL e quindi sp_addextendedproc per registrarla di nuovo specificando il percorso completo.  
  
 Il nome della funzione specificato in `sp_addextendedproc` deve corrispondere esattamente a quello presente nella DLL, anche nell'uso di maiuscole e minuscole. Il comando seguente, ad esempio, registra una funzione `xp_hello,` che si trova in una dll denominata `xp_hello.dll` come stored procedure estesa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL12.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 Se il nome della funzione specificato in `sp_addextendedproc` non corrisponde esattamente al nome presente nella DLL, il nuovo nome verrà registrato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma non sarà possibile utilizzarlo. Se, ad esempio `xp_Hello` , viene registrato come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stored procedure esteso disponibile in `xp_hello.dll`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sarà in grado di trovare la funzione nella dll se si utilizza `xp_Hello` per chiamare la funzione in un secondo momento.  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 Se il nome della funzione specificato in `sp_addextendedproc` corrisponde esattamente al nome della funzione nella DLL e per le regole di confronto dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene fatta distinzione tra maiuscole e minuscole, l'utente può chiamare la stored procedure estesa utilizzando una qualsiasi combinazione di lettere maiuscole e minuscole per il nome.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 Quando le regole di confronto dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza fanno distinzione tra maiuscole [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e minuscole, non sarà in grado di chiamare il stored procedure esteso, anche se è stato registrato con lo stesso nome e le stesse regole di confronto della funzione nella dll, se la procedura viene chiamata con un case diverso.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 Non è necessario arrestare e riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedi anche  
 [sp_addextendedproc &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
