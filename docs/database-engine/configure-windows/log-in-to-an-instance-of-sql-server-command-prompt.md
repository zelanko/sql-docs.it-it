---
title: Accedere a un'istanza di SQL Server (prompt dei comandi) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 080c90dca2ff47c4ef217beda703615b59996112
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785228"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Log In to an Instance of SQL Server (Command Prompt)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
  
