---
title: Accedere a un'istanza di SQL Server (prompt dei comandi) | Microsoft Docs
description: Informazioni sull'utilità "sqlcmd". Scoprire come usarla in un prompt dei comandi per testare la connettività con un'istanza di SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0723a5d463757eca93dd7bacb1fc2b8fe232cdd8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772403"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Log In to an Instance of SQL Server (Command Prompt)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento viene illustrato come eseguire il test di connettività a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare l'utilità **sqlcmd** .  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>Per accedere all'istanza predefinita di SQL Server  
  
1.  Al prompt dei comandi digitare il comando seguente per connettersi mediante l'autenticazione di Windows:  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>Per accedere a un'istanza denominata di SQL Server  
  
1.  Al prompt dei comandi digitare il comando seguente per connettersi mediante l'autenticazione di Windows:  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità sqlcmd](../../tools/sqlcmd-utility.md)   
 [Utilità osql](../../tools/osql-utility.md)  
  
  
