---
title: Gestire i file di log DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c32c76188ec7a685ecaa117ea303673bf4d3e682
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616931"
---
# <a name="manage-dqs-log-files"></a>Gestire i file di log DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  I file di log di[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) consentono di diagnosticare e risolvere i problemi con il [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e il [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. Vengono generati file di log separati per il [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e il [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
 È possibile utilizzare il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] per configurare l'impostazione di gravità del log per le funzionalità e i moduli del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Inoltre, è possibile configurare anche altre impostazioni (avanzate) per i file di log DQS modificando manualmente le impostazioni di configurazione del log DQS nel database DQS_MAIN e in un file XML nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="DQSServer"></a> File di log del server Data Quality  
 Il file di log del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , DQServerLog.DQS_MAIN.log, include i log delle attività eseguite nel [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Se è stata installata l'istanza predefinita di SQL Server, il file DQServerLog.DQS_MAIN.log è disponibile in C:\Programmi\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log. Il file di log del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] contiene le informazioni seguenti, ognuna delimitata da una pipe (|):  
  
-   Date e Time  
  
-   Nome del thread  
  
-   ID del thread  
  
-   Gravità del log (ERRORE IRREVERSIBILE, ERRORE, AVVISO, INFORMAZIONI e DEBUG)  
  
    > [!NOTE]  
    >  DEBUG corrisponde a Dettagliato.  
  
-   UID (ID interno dell'infrastruttura DQS)  
  
-   Namespace  
  
-   Classe e metodo  
  
-   Message  
  
 Oltre a questi valori, nel file di log vengono visualizzate anche informazioni sulla versione dell'applicazione, il nome del computer, il nome dell'utente e il sistema operativo.  
  
 Una voce di esempio nel file di log del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] è simile alla seguente:  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 Il file DQServerLog.DQS_MAIN.log è un file mobile e quando il file di log esistente supera il limite delle dimensioni dei file mobili specificate nelle impostazioni di configurazione di log del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] viene creato un nuovo file di log. Per ulteriori informazioni, vedere [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="DQSClient"></a> File di log del client Data Quality  
 Il file di log del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , DQClientLog.log, include i log lato client. Il file di log del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] è disponibile in %APPDATA%\SSDQS\Log. Il file di log del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] contiene un set di informazioni simili a quelle del file di log del server, ma per il lato client.  
  
 Analogamente al file di log del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , anche il file di log del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] è un file mobile e quando il file di log esistente supera il limite delle dimensioni dei file mobili specificate nelle impostazioni di configurazione di log del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] viene creato un nuovo file di log. Per ulteriori informazioni, vedere [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="DQSCleansing"></a> File di log del componente DQS Cleansing  
 Il file di log del [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] , DQSSSISLog.log, include i log delle attività eseguite utilizzando il [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. Il file di log del componente [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] è disponibile in %APPDATA%\SSDQS\Log. Il file di log di [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] contiene un set di informazioni simili a quelle del file di log del server, ma per [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
##  <a name="RT"></a> Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Descrive come configurare le impostazioni di gravità del log per file di log DQS utilizzando il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Configurare livelli di gravità per i file di log DQS](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Descrive come configurare manualmente le impostazioni avanzate per i file di log DQS.|[Configurare le impostazioni avanzate per i file di log DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione DQS](../data-quality-services/dqs-administration.md)  
  
  
