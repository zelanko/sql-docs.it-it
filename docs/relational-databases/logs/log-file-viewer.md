---
title: Visualizzatore file di log | Microsoft Docs
description: Usare il visualizzatore file di log in SQL Server Management Studio per informazioni relative a errori ed eventi acquisite in file di log.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer
ms.assetid: a4ea7fc8-1cb2-4c98-bc86-8991c5e748b2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7425bb2175b9a2e7b813f63e7d78aec7e73ef5ec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85668123"
---
# <a name="log-file-viewer"></a>Visualizzatore file di log
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  È possibile utilizzare il Visualizzatore file di log in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per accedere alle informazioni relative a errori ed eventi acquisite nei file di log.  
  
## <a name="benefits-of-using-log-file-viewer"></a>Vantaggi dell'utilizzo del Visualizzatore file di log  
 È possibile visualizzare i file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un'istanza locale o remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando l'istanza di destinazione è offline o non può essere avviata. È possibile accedere ai file di log offline tramite lo strumento Server registrati o a livello di codice tramite query WMI e WQL (WMI Query Language). Per altre informazioni, vedere [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md). Di seguito vengono indicati i tipi di file di log a cui è possibile accedere utilizzando il Visualizzatore file di log:  
  
-   Raccolta controlli  
  
-   Raccolta di dati  
  
-   Posta elettronica database  
  
-   Cronologia processi  
  
-   Piani di manutenzione  
  
-   Piani di manutenzione remoti  
  
-   SQL Server  
  
-   SQL Server Agent  
  
-   Windows NT (eventi di Windows a cui è possibile accedere dal Visualizzatore eventi di Windows)  
  
## <a name="log-file-viewer-tasks"></a>Attività del Visualizzatore file di log  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come aprire il Visualizzatore file di log, a seconda delle informazioni da visualizzare.|[Aprire il visualizzatore file di log](../../relational-databases/logs/open-log-file-viewer.md)|  
|Viene descritto come visualizzare file di log offline tramite server registrati e come verificare autorizzazioni WMI.|[Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md)|  
|Viene fornita la Guida sensibile al contesto del Visualizzatore file di log.|[Guida sensibile al contesto del Visualizzatore file di log](../../relational-databases/logs/log-file-viewer-f1-help.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Log degli errori di SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
  
