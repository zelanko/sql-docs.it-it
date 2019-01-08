---
title: Aggiornare lo schema dei database DQS dopo l'installazione dell'aggiornamento di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4d4f5af2a9b0c58e8cef89f143e4ec42cb03695
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372923"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>Aggiornare lo schema dei database DQS dopo l'installazione dell'aggiornamento di SQL Server
  Dopo aver installato un aggiornamento di SQL Server (patch, hotfix o aggiornamento cumulativo) in un'istanza di DQS configurata precedentemente, potrebbe essere necessario aggiornare lo schema dei database DQS eseguendo il file DQSInstaller.exe con il parametro della riga di comando **upgrade**. In caso contrario, potrebbe essere visualizzato l'errore seguente durante il tentativo di connessione al server Data Quality utilizzando il client Data Quality:  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 L'aggiornamento dello schema dei database DQS non influisce sui dati esistenti nei database DQS (Knowledge Base, progetti Data Quality e risultati esportati nel database DQS_STAGING_DATA). Tuttavia, è necessario eseguire il backup dei database DQS prima di aggiornare il relativo schema per evitare eventuali perdite di dati accidentali durante l'aggiornamento dello schema. Per altre informazioni sul ripristino dei database DQS, vedere [Backup e ripristino di database DQS](../backing-up-and-restoring-dqs-databases.md).  
  
> [!NOTE]  
>  Per la maggior parte degli aggiornamenti di SQL Server è richiesto un aggiornamento allo schema dei database DQS. Per informazioni sugli aggiornamenti di SQL Server che verrà richiesto un aggiornamento allo schema dei database DQS, vedere il grafico nel passaggio 1.A in [aggiornare DQS: Installazione di aggiornamenti cumulativi o patch di Hotfix in Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario aver eseguito l'accesso come membro del gruppo di amministratori nel computer di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   È necessario che l'account utente di Windows sia membro del ruolo predefinito del server sysadmin nell'istanza di SQL Server in cui è installato [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
### <a name="to-upgrade-dqs-databases-schema"></a>Per aggiornare lo schema dei database DQS  
  
1.  (Opzione consigliata) Eseguire il backup dei database DQS prima di procedere con l'aggiornamento dello schema. Per altre informazioni sul ripristino dei database DQS, vedere [Backup e ripristino di database DQS](../backing-up-and-restoring-dqs-databases.md).  
  
2.  Avviare il prompt dei comandi.  
  
3.  Al prompt dei comandi impostare la directory sul percorso in cui è disponibile il file DQSInstaller.exe. Se è stata installata l'istanza predefinita di SQL Server, il file DQSinstaller.exe sarà disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  Al prompt dei comandi digitare il comando seguente e premere INVIO:  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  Tramite il programma di installazione viene richiesta all'utente la conferma dell'esecuzione del backup dei database DQS prima di continuare. Se il backup dei database DQS è già stato eseguito, digitare `Y` o `Yes` e premere INVIO per continuare l'aggiornamento.  
  
6.  Se l'aggiornamento dello schema dei database DQS viene terminato correttamente, viene visualizzato un messaggio di completamento.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Accedere al server Data Quality aggiornato da un'applicazione client Data Quality.  
  
 Per altre informazioni sull'aggiornamento di DQS Aggiorna lo schema dei database dopo l'installazione di SQL Server e dei relativi passaggi di risoluzione dei problemi, vedere [aggiornare DQS: Installazione di aggiornamenti cumulativi o patch di Hotfix in Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare Data Quality Services](install-data-quality-services.md)   
 [Aggiornare gli assembly SQLCLR dopo l'aggiornamento di .NET Framework](upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
