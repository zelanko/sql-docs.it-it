---
title: Aprire il Visualizzatore File di Log | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer, opening
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9e76c7eb85306f63e9be230c76159efbab25444a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083977"
---
# <a name="open-log-file-viewer"></a>Aprire il visualizzatore file di log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile utilizzare il Visualizzatore file di log in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per accedere alle informazioni relative a errori ed eventi acquisite nei log seguenti:  
  
-   Raccolta controlli  
  
-   Raccolta dati  
  
-   Posta elettronica database  
  
-   Cronologia processi  
  
-   SQL Server  
  
-   SQL Server Agent  
  
-   Eventi di Windows. È possibile accedere a tali eventi anche dal Visualizzatore eventi.  
  
 A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], è possibile utilizzare Server registrati per visualizzare file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da istanze locali o remote di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usando Server registrati, è possibile visualizzare i file di log quando le istanze sono online o offline. Per altre informazioni sull'accesso online, vedere la procedura "Per visualizzare file di log online dalla finestra Server registrati" più avanti in questo argomento. Per altre informazioni su come accedere offline a file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
 È possibile aprire il Visualizzatore file di log in diversi modi, a seconda delle informazioni che si desidera visualizzare.  
  
##  <a name="BeforeYouBegin"></a> Autorizzazioni  
 Per accedere ai file di log per le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] online, è necessaria l'appartenenza al ruolo predefinito del server securityadmin.  
  
 Per accedere a file di log per istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline, è necessario avere accesso in lettura sia allo spazio dei nomi WMI **Root\Microsoft\SqlServer\ComputerManagement10** sia alla cartella in cui sono archiviati i file di log. Per altre informazioni, vedere la sezione Autorizzazioni dell'argomento [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
### <a name="security"></a>Security  
 È necessaria l'appartenenza al ruolo predefinito del server securityadmin.  
  
### <a name="view-log-files"></a>Visualizzare file di log  
  
##### <a name="to-view-logs-that-are-related-to-general-sql-server-activity"></a>Per visualizzare log relativi all'attività generale di SQL Server  
  
1.  In Esplora oggetti espandere **Gestione**.  
  
2.  Effettuare una delle operazioni seguenti:  
  
    -   Fare clic con il pulsante destro del mouse su **Log di SQL Server**, scegliere **Visualizza**, quindi fare clic su **Log di SQL Server** o su **Log di SQL Server e di Windows**.  
  
    -   Espandere **Log di SQL Server**, fare clic con il pulsante destro del mouse su un file di log, quindi scegliere **Visualizza log di SQL Server**. È anche possibile fare doppio clic su un file di log.  
  
     I log includono **Posta elettronica database**, **SQL Server**, **SQL Server Agent**e **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-jobs"></a>Per visualizzare log relativi ai processi  
  
-   In Esplora oggetti espandere **SQL Server Agent**, fare clic con il pulsante destro del mouse su **Processi**, quindi scegliere **Visualizza cronologia**.  
  
     I log includono **Posta elettronica database**, **Cronologia processi**e **SQL Server Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-maintenance-plans"></a>Per visualizzare log relativi ai piani di manutenzione  
  
-   In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Piani di manutenzione**, quindi scegliere **Visualizza cronologia**.  
  
     I log includono **Posta elettronica database**, **Cronologia processo**, **Piani di manutenzione**, **Piani di manutenzione remoti**e **SQL Server Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-data-collection"></a>Per visualizzare log relativi alla raccolta dati  
  
-   In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Raccolta dati**, quindi scegliere **Visualizza log**.  
  
     I log includono **Raccolta dati**, **Cronologia processo**e **SQL Server Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-database-mail"></a>Per visualizzare log relativi a Posta elettronica database  
  
-   In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Posta elettronica database**, quindi scegliere **Visualizza log Posta elettronica database**.  
  
     I log includono **Posta elettronica database, Cronologia processo**, **Piani di manutenzione**, **Piani di manutenzione remoti**, **SQL Server**, **SQL Server Agent**e **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>Per visualizzare log relativi alle raccolte di controlli  
  
-   In Esplora oggetti espandere **Sicurezza**, espandere **Controlli**, fare clic con il pulsante destro del mouse su un controllo, quindi scegliere **Visualizza log di controllo**.  
  
     I log includono **Raccolta controlli** e **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>Per visualizzare log relativi alle raccolte di controlli  
  
-   In Esplora oggetti espandere **Sicurezza**, espandere **Controlli**, fare clic con il pulsante destro del mouse su un controllo, quindi scegliere **Visualizza log di controllo**.  
  
     I log includono **Raccolta controlli** e **Windows NT**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzatore file di log](../../relational-databases/logs/log-file-viewer.md)   
 [SQL Server Audit &#40;Motore di database&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
