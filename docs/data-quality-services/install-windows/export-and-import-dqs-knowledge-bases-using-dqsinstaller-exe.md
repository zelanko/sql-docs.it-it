---
title: Esportare e importare le Knowledge base di DQS utilizzando DQSInstaller. exe
description: Informazioni su come utilizzare DQSInstaller. exe per esportare e importare le Knowledge base di DQS per SQL Server Data Quality Services (DQS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ae87b9daebdef6b81c4d96abc253820cf7cb8228
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75558144"
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Esportare e importare le Knowledge Base di DQS con DQSInstaller.exe

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Per un'installazione esistente di DQS, è possibile esportare contemporaneamente tutte le Knowledge Base presenti in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in un file di backup DQS (con estensione dqsb) e quindi utilizzare successivamente il file con estensione dqsb per importare contemporaneamente tutte le Knowledge Base presenti in un'istanza diversa di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] eseguendo il file DQSInstaller.exe dal prompt dei comandi. Per ulteriori informazioni sull'esecuzione di DQSInstaller.exe dal prompt dei comandi, vedere [Eseguire DQSInstaller.exe dal prompt dei comandi](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) in [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
 Questa funzionalità consente di eseguire un backup di *tutte* le Knowledge Base in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] contemporaneamente senza dovere esportare singolarmente ogni Knowledge Base in un file con estensione dqs tramite [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Allo stesso modo, è possibile importare contemporaneamente *tutte* le Knowledge Base dal file di backup in un altro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] senza dovere importare singolarmente ogni Knowledge Base da un file con estensione dqs tramite [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Tale operazione è particolarmente utile per eseguire il backup e il ripristino delle Knowledge Base quando si disinstalla [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] su un computer e quindi per reinstallarlo su un computer diverso. È possibile esportare facilmente tutte le Knowledge Base presenti in un'installazione esistente di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in un file di backup (con estensione dqsb) DQS, quindi importare tutte le Knowledge Base dal file di backup dopo avere installato [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] su un computer diverso.  
  
##  <a name="export"></a>Esportazione di Knowledge base in un file con estensione dqsb  
 È possibile esportare in qualsiasi momento tutte le Knowledge Base nel [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] esistente o durante la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].  
  
-   Per esportare tutte le Knowledge Base presenti in un [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in un file di backup (con estensione dqsb) DQS, eseguire DQSInstaller.exe con il parametro `exportkbs` dal prompt dei comandi, insieme al percorso completo e al nome file dove si desidera esportare le Knowledge Base. Ad esempio, per esportare tutte le Knowledge Base nel file DQSBackup.dqsb nell'unità C:  
  
    ```  
    dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Se il nome file fornito già esiste nel percorso specificato, il programma di installazione richiederà se ricoprire il file.  
  
-   Per esportare tutte le Knowledge Base presenti in un file di backup DQS durante la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], eseguire DQSInstaller.exe con il parametro `uninstall` dal prompt dei comandi, insieme al percorso completo e al nome file dove si desidera esportare le Knowledge Base. Ad esempio, per esportare tutte le Knowledge Base nel file DQSBackup.dqsb nell'unità C: e quindi disinstallare [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]:  
  
    ```  
    dqsinstaller.exe -uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Se non si specificano il percorso completo e il nome file del file di backup DQS durante la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] dal prompt dei comandi utilizzando il parametro `uninstall` , viene visualizzato un messaggio in cui viene segnalato che tutte le Knowledge Base verranno eliminate e che consente di scegliere se proseguire il processo di disinstallazione.  
  
##  <a name="import"></a>Importazione di Knowledge base dal file dqsb  
 È possibile importare tutte le Knowledge Base da un file di backup DQS (con estensione dqsb) dopo aver completato l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Per importare le Knowledge Base, è necessario disporre di un file di backup DQS valido (con estensione dqsb).  
  
 Eseguire il file DQSInstaller.exe con il parametro `importkbs` dal prompt dei comandi, insieme al percorso completo e al nome file da cui si desidera importare le Knowledge Base. Ad esempio, per importare tutte le Knowledge Base dal file DQSBackup.dqsb nell'unità C:  
  
```  
dqsinstaller.exe -importkbs c:\DQSBackup.dqsb  
```  
  
 Se vi sono Knowledge Base in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] con lo stesso nome di quelle che si stanno importando, i nomi delle Knowledge Base importate saranno accodati con un carattere di sottolineatura (_) seguito da un valore intero che inizia con 1. Ad esempio, se il dominio "CompanyName" è duplicato, il nome di dominio importato sarà "CompanyName_1".  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire DQSInstaller. exe per completare l'installazione del server Data Quality](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Installare Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Esportare una Knowledge base in un file DQS](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [Importazione di una Knowledge Base da un file DQS](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
