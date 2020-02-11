---
title: Rimuovere oggetti server Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f273823825cf94da6269a58389f04207ad1c2707
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68190681"
---
# <a name="remove-data-quality-server-objects"></a>Rimuovere oggetti server Data Quality Services
  La disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o la rimozione completa di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è disponibile [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] non comporta l'eliminazione di alcun oggetto [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , inclusi i database DQS. Questo implica che non si perdono i dati DQS se si disinstalla [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] utilizzando il programma di installazione di SQL Server. È pertanto necessario eliminare manualmente questi oggetti [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] una volta completato il processo di disinstallazione.  
  
> [!NOTE]
>  -   Prima di disinstallare [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], si consideri di eseguire il backup di tutte le Knowledge Base esistenti esportandolo in un file con estensione dqsb e di utilizzare il file in un secondo momento per importare di nuovo tutte le Knowledge Base in una nuova installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . L'esportazione e l'importazione di tutte le Knowledge Base DQS possono essere effettuate solo eseguendo DQSInstaller.exe con i parametri della riga di comando appropriati dal prompt dei comandi. Per altre informazioni, vedere [Esportare e importare le Knowledge Base di DQS utilizzando DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).  
> -   Prima di eliminare i database DQS, si consideri di eseguire il backup dei database se si desidera conservarlo e utilizzarlo in un secondo momento per ripristinare i dati. Per informazioni su questa operazione, vedere [Gestire i database DQS](../../../2014/data-quality-services/manage-dqs-databases.md).  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>Disinstallare il server DQS da un'istanza di SQL Server.  
 Se si disinstalla solo [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario eliminare manualmente gli oggetti [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] seguenti dall'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dopo aver completato il processo di disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] :  
  
-   Database DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA.  
  
-   \#Account di accesso #MS_dqs_db_owner_login## e ##MS_dqs_service_login##.  
  
-   Stored procedure DQInitDQS_MAIN dal database master.  
  
 È possibile eliminare questi oggetti in SQL Server Management Studio facendo clic con il pulsante destro del mouse sull'oggetto e scegliendo **Elimina** del menu di scelta rapida.  
  
> [!IMPORTANT]  
>  Se si disinstalla solo [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] da un'istanza di SQL Server utilizzando il parametro della riga di comando `-uninstall` dal prompt dei comandi, tutti gli oggetti DQS vengono eliminati come parte del processo di disinstallazione. Non è necessario eliminarli manualmente dopo la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. Per disinstallare [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] dal prompt dei comandi, digitare il comando seguente al prompt dei comandi e premere INVIO:   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>Disinstallare l'istanza di SQL Server contenente il server DQS  
 Se si disinstalla completamente l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è presente [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], è necessario eliminare manualmente i database DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA dal computer dopo il completamento del processo di disinstallazione. Per un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinita, i file dei database DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA sono disponibili in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA.  
  
## <a name="see-also"></a>Vedere anche  
 [Disinstallare un'istanza esistente di SQL Server &#40;Programma di installazione&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [Disinstallare SQL Server 2014](uninstall-sql-server.md)  
  
  
