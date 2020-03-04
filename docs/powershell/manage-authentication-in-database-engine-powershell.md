---
title: "PowerShell: Gestire l'autenticazione"
titleSuffix: SQL Server on Linux
description: Informazioni su come usare PowerShell per gestire l'autenticazione di Windows e SQL per SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 22c48323aa7570440a3edb06400d9a96e9bd9924
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75557966"
---
# <a name="powershell-manage-authentication-to-sql-server"></a>PowerShell: Gestire l'autenticazione per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Per impostazione predefinita, i componenti PowerShell di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzano l'autenticazione di Windows in caso di connessione a un'istanza del [!INCLUDE[ssDE](../includes/ssde-md.md)]. È possibile usare l'autenticazione di SQL Server definendo un'unità virtuale PowerShell o specificando i parametri **-Username** e **-Password** per **Invoke-Sqlcmd**.  
  
> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).

  
##  <a name="Permissions"></a> Autorizzazioni  
 Tutte le azioni eseguibili in un'istanza del [!INCLUDE[ssDE](../includes/ssde-md.md)] vengono controllate dalle autorizzazioni concesse alle credenziali di autenticazione utilizzate per connettersi all'istanza. Per impostazione predefinita, il provider e i cmdlet di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzano l'account di Windows in esecuzione per eseguire una connessione con autenticazione di Windows al [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
 Per effettuare una connessione con autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è necessario fornire un ID di accesso per l'autenticazione di SQL Server e una password. Se si usa il provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è necessario associare le credenziali di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un'unità virtuale e quindi usare il comando di modifica della directory (**cd**) per stabilire la connessione a tale unità. In Windows PowerShell le credenziali di sicurezza possono essere associate solo a unità virtuali.  
  
##  <a name="SQLAuthVirtDrv"></a> Autenticazione di SQL Server tramite un'unità virtuale  
 **Per creare un'unità virtuale associata a un accesso di autenticazione di SQL Server**  
  
1.  Creare una funzione che:  
  
    1.  Disponga di parametri per il nome da assegnare all'unità virtuale, l'ID di accesso e il percorso del provider da associare all'unità virtuale.  
  
    2.  Usi **read-host** per richiedere all'utente la password.  
  
    3.  Usi **new-object** per creare un oggetto credenziali.  
  
    4.  Usi **new-psdrive** per creare un'unità virtuale con le credenziali fornite.  
  
2.  Richiamare la funzione per creare un'unità virtuale con le credenziali fornite.  
  
### <a name="example-virtual-drive"></a>Esempio (unità virtuale)  
 In questo esempio viene creata una funzione denominata **sqldrive** che può essere utilizzata per creare un'unità virtuale associata all'account di accesso con autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e all'istanza specificati.  
  
 La funzione **sqldrive** richiede di immettere la password per effettuare l'accesso, mascherandola durante la digitazione. Quando si usa il comando di modifica della directory (**cd**) per connettersi a un percorso usando il nome di unità virtuale, tutte le operazioni vengono eseguite usando le credenziali di accesso con autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornite al momento della creazione dell'unità.  
  
```  
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = read-host -AsSecureString -Prompt "Password"  
    $cred = new-object System.Management.Automation.PSCredential -argumentlist $login,$pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> Autenticazione di SQL Server tramite Invoke-Sqlcmd  
 **Per utilizzare Invoke-Sqlcmd con l'autenticazione di SQL Server**  
  
1.  Usare il parametro **-Username** per specificare un ID di accesso e il parametro **-Password** per specificare la password associata.  
  
### <a name="example-invoke-sqlcmd"></a>Esempio (Invoke-Sqlcmd)  
 In questo esempio viene utilizzato l'host della lettura cmdlet per la richiesta di una password all'utente, quindi viene stabilita la connessione tramite l'autenticazione di SQL Server.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [Provider PowerShell per SQL Server](sql-server-powershell-provider.md)   
 [Cmdlet Invoke-Sqlcmd](invoke-sqlcmd-cmdlet.md)  
  
  
