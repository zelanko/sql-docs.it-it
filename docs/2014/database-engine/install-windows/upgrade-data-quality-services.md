---
title: Aggiornare Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c76fda112acae7b8a9314d217f5c32d197e87f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62775631"
---
# <a name="upgrade-data-quality-services"></a>Aggiornare Data Quality Services
  In questo argomento vengono fornite le informazioni su come aggiornare l'installazione esistente di Data Quality Services (DQS) a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Come parte dell'aggiornamento di Data Quality Server in DQS a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è inoltre necessario aggiornare lo schema dei database DQS.  
  
> [!IMPORTANT]
>  -   Per evitare eventuali perdite di dati accidentali durante l'aggiornamento dello schema, è necessario eseguire il backup dei database DQS prima di aggiornare DQS. Per altre informazioni sul ripristino dei database DQS, vedere [Backup e ripristino di database DQS](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
> -   È possibile connettersi alla versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Data Quality Server usando la versione corrente o una precedente del client Data Quality o [Trasformazione DQS Cleansing](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) in Integration Services per eseguire le attività relative alla qualità dei dati.  
> -   È possibile continuare a utilizzare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del componente aggiuntivo Master Data Services per Excel dopo l'aggiornamento di Data Quality Services e di Master Data Services a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Tuttavia, una versione precedente del componente aggiuntivo Master Data Services per Excel non funzionerà dopo l'aggiornamento a SQL Server 2014 CTP2. È possibile scaricare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del componente aggiuntivo Master Data Services per Excel da [qui](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario aver eseguito l'accesso come membro del gruppo di amministratori nel computer di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   È necessario che l'account utente di Windows sia membro del ruolo predefinito del server sysadmin nell'istanza di SQL Server in cui è installato [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
##  <a name="Upgrade"></a> Aggiornamento di DQS  
 Per aggiornare DQS:  
  
1.  Eseguire il backup dei database DQS prima di avviare il processo di aggiornamento. Per altre informazioni sul ripristino dei database DQS, vedere [Backup e ripristino di database DQS](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Aggiornare l'istanza di SQL Server dove DQS è installato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Eseguire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  Fare clic su **Installazione**nel riquadro sinistro.  
  
    3.  Nel riquadro di destra fare clic su **Aggiorna da SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 o SQL Server 2012**.  
  
    4.  Completare l'Installazione guidata.  
  
        > [!NOTE]  
        >  Verrà aggiornata l'istanza di SQL Server a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ; inoltre, verrà installato il client Data Quality più recente, se questo client è stato precedentemente installato nel computer. Se il client Data Quality è stato installato in altri computer, è necessario eseguire i passaggi secondari nel passaggio 2 nei computer in questione per installare la versione corrente del client Data Quality. Tramite l'Installazione guidata viene installata la versione corrente del client Data Quality, insieme alla versione esistente di questo client. Al termine dell'aggiornamento dello schema dei database DQS, è possibile connettersi alla versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Data Quality Server utilizzando la versione corrente o una precedente del client Data Quality.  
  
3.  Aggiornare lo schema dei database DQS.  
  
    1.  Avviare il prompt dei comandi come amministratore.  
  
    2.  Al prompt dei comandi impostare la directory sul percorso in cui è disponibile il file DQSInstaller.exe. Per l'istanza predefinita di SQL Server, il file DQSinstaller.exe è disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  Al prompt dei comandi digitare il comando seguente e premere INVIO:  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  Tramite il programma di installazione viene richiesta all'utente la conferma dell'esecuzione del backup dei database DQS prima di continuare. Se il backup dei database DQS è già stato eseguito, digitare `Y` o `Yes`, quindi premere INVIO per continuare l'aggiornamento.  
  
    5.  Se l'aggiornamento dello schema dei database DQS viene terminato correttamente, viene visualizzato un messaggio di completamento.  
  
##  <a name="Verify"></a> Verifica dell'aggiornamento dello schema dei database DQS  
 Per verificare che lo schema dei database DQS sia stato aggiornato correttamente, è possibile controllare la versione corrente nei database DQS_MAIN e DQS_PROJECTS eseguendo una query sulla tabella A_DB_VERSION in ogni database. A tale scopo, procedere come indicato di seguito:  
  
1.  Avviare SQL Server Management Studio e connettersi all'istanza di SQL Server contenente lo schema dei database DQS aggiornato.  
  
2.  Eseguire la query riportata di seguito:  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  Nell'output verrà visualizzata una voce per ogni aggiornamento, insieme alla data di aggiornamento. Il valore massimo di VERSION_ID e ASSEMBLY_VERSION nella data più recente è la versione corrente. Un valore pari a 2 nella colonna STATUS indica l'esito positivo. Se si è verificato un errore, questo verrà visualizzato nella colonna ERROR. Esempio di output:  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATO|ERRORE|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMINIO\NomeUtente>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMINIO\NomeUtente>|2||  
  
## <a name="see-also"></a>Vedere anche  
 [Installare Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Rimuovere oggetti server Data Quality Services](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Eseguire l'aggiornamento a SQL Server 2014](upgrade-sql-server.md)  
  
  
