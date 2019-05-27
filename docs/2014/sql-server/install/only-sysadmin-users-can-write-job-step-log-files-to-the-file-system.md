---
title: Solo gli utenti sysadmin possono scrivere file di log di passaggio di processo nel file System | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84d04729e2f4c00c5d127a706727567c44855cd6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093676"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>Solo gli utenti sysadmin possono scrivere file di log dei passaggi del processo nel file system
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] scrive facoltativamente un log per ogni passaggio del processo.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Descrizione  
 Nelle [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può scrivere log nel file System per i processi che sono proprietà dei membri delle **sysadmin** ruolo predefinito del server. Se il proprietario del processo non è un membro del **sysadmin** ruolo e se l'account proxy è abilitato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può scrivere log nel file System utilizzando le credenziali dell'account proxy.  
  
 Dopo l'aggiornamento, i processi che appartengono a utenti che non sono membri del **sysadmin** ruolo predefinito del server non possono più scrivere log nel file System. Al contrario, questi utenti possono selezionare l'opzione per scrivere i log in una tabella nel **msdb** database. I membri del **sysadmin** ruolo può ancora scrivere file di log nel file System.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Dopo l'aggiornamento, i processi che appartengono a utenti che non sono membri del **sysadmin** ruolo continueranno a essere eseguite, ma non verranno creati i log. Per registrare i passaggi del processo in una tabella, gli utenti che non sono membri del **sysadmin** ruolo necessario aggiornare manualmente i processi.  
  
 Per ulteriori informazioni, vedere gli argomenti "Creazione di processi", "Creazione di passaggi di processo" e "Gestione di più passaggi di processo" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
