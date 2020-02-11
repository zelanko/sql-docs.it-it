---
title: Solo gli utenti sysadmin possono scrivere file di log dei passaggi del processo nel file system | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093676"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>Solo gli utenti sysadmin possono scrivere file di log dei passaggi del processo nel file system
  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] scrive facoltativamente un log per ogni passaggio del processo.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agente  
  
## <a name="description"></a>Descrizione  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può scrivere log nel file System per i processi di proprietà dei membri del ruolo predefinito del server **sysadmin** . Se il proprietario del processo non è un membro del ruolo **sysadmin** e se l'account proxy è abilitato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può scrivere i log nel file System usando le credenziali dell'account proxy.  
  
 Dopo l'aggiornamento, i processi di proprietà di utenti che non sono membri del ruolo predefinito del server **sysadmin** non possono più scrivere log nel file System. Questi utenti possono invece selezionare l'opzione per scrivere i log in una tabella del database **msdb** . I membri del ruolo **sysadmin** possono comunque scrivere i file di log nel file System.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Dopo l'aggiornamento, i processi di proprietà di utenti che non sono membri del ruolo **sysadmin** continueranno a essere eseguiti, ma i registri non verranno creati. Per registrare i passaggi del processo in una tabella, gli utenti che non sono membri del ruolo **sysadmin** devono aggiornare manualmente i processi.  
  
 Per ulteriori informazioni, vedere gli argomenti "Creazione di processi", "Creazione di passaggi di processo" e "Gestione di più passaggi di processo" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
