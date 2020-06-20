---
title: Aggiornare gli assembly SQLCLR dopo l'aggiornamento di .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b1a008cc-7e6b-4655-a869-bd429f986400
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dbdd0f502f97d1329072a319648c50b48ac583ff
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937562"
---
# <a name="upgrade-sqlclr-assemblies-after-net-framework-update"></a>Aggiornare gli assembly SQLCLR dopo l'aggiornamento di .NET Framework
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) è una raccolta di routine SQLCR (SQL Common Language Runtime) che fanno riferimento agli assembly Microsoft .NET Framework 4. Quando si installano aggiornamenti di .NET Framework nel computer che possono interessare un assembly .NET Framework di riferimento di questo tipo, tale operazione comporta una modifica nell'ID della versione del modulo (MVID, Module Version ID) dell'assembly nel Global Assembly Cache (GAC). Questa modifica determina una mancata corrispondenza tra i MVID dell'assembly a cui si fa riferimento nella GAC e l'assembly in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se per l'aggiornamento di .NET Framework viene richiesto il riavvio del computer di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , gli assembly SQLCLR interessati vengono aggiornati automaticamente per correggere il problema di mancata corrispondenza di MVID al riavvio di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Per gli aggiornamenti di .NET Framework per cui non è richiesto il riavvio del computer di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , si verifica tuttavia un errore a causa della mancata corrispondenza nei MVID degli assembly quando si tenta di connettersi a [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] tramite [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]:  
  
```  
A new version of .NET was installed on this machine. In order to continue to work with DQS please run dqsinstaller.exe -upgradedlls.  
```  
  
 Per correggere questo problema, è necessario aggiornare gli assembly SQLCLR interessati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . È possibile eseguire questa operazione eseguendo il file DQSInstaller.exe con il parametro della riga di comando **upgradedlls** per ignorare la ricreazione di database di DQS e aggiornare solo gli assembly interessati. In questo modo viene garantita l'integrità della Knowledge Base, dei progetti Data Quality e di qualsiasi altro dato di DQS.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario aver eseguito l'accesso come membro del gruppo di amministratori nel computer di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   È necessario che l'account utente di Windows sia membro del ruolo predefinito del server sysadmin nell'istanza di SQL Server in cui è installato [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
### <a name="to-upgrade-sqlclr-assemblies"></a>Per aggiornare gli assembly SQLCLR  
  
1.  Avviare il prompt dei comandi.  
  
2.  Al prompt dei comandi impostare la directory sul percorso in cui è disponibile il file DQSInstaller.exe. Se è stata installata l'istanza predefinita di SQL Server, il file DQSinstaller.exe sarà disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  Al prompt dei comandi digitare il comando seguente e premere INVIO:  
  
    ```  
    dqsinstaller.exe -upgradedlls  
    ```  
  
4.  I passaggi rimanenti sono uguali ai passaggi 2-6 della sezione [Eseguire DQSInstaller.exe dalla schermata Start, dal menu Start o da Esplora risorse](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer) in [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare Data Quality Services](install-data-quality-services.md)   
 [Aggiornare lo schema dei database DQS dopo l'installazione dell'aggiornamento di SQL Server](upgrade-dqs-databases-schema-after-installing-sql-server-update.md)  
  
  
