---
title: Creare un ambiente multiserver | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c5c59a8802597b893110a5f2c26c919c16c8e83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192966"
---
# <a name="create-a-multiserver-environment"></a>Creazione di un ambiente multiserver
  L'amministrazione multiserver richiede l'impostazione di un server master (MSX) e di uno o più server di destinazione (TSX). I processi che verranno eseguiti in tutti i server di destinazione vengono innanzitutto definiti nel server master e quindi scaricati nei server di destinazione.  
  
 Per impostazione predefinita, per le connessioni tra server master e server di destinazione sono abilitate la crittografia SSL (Secure Sockets Layer) completa e la convalida del certificato. Per altre informazioni, vedere [Impostazione delle opzioni di crittografia nei server di destinazione](set-encryption-options-on-target-servers.md).  
  
 Se si dispone di un numero elevato di server di destinazione, evitare di definire il server master in un server di produzione con requisiti di prestazioni significativi da altre funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , perché il traffico del server di destinazione può rallentare le prestazioni nel server di produzione. Se si inoltrano anche gli eventi a un server master dedicato, è possibile centralizzare l'intera amministrazione in un singolo server. Per altre informazioni, vedere [Gestire eventi](manage-events.md).  
  
> [!NOTE]  
>  Per usare l'elaborazione dei processi multiserver, l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere membro del ruolo **TargetServersRole** del database **msdb** nel server master. Tramite Configurazione guidata server master l'account del servizio viene automaticamente aggiunto a questo ruolo all'interno del processo di integrazione.  
  
## <a name="considerations-for-multiserver-environments"></a>Considerazioni relative agli ambienti multiserver  
 Vedere la tabella seguente per le configurazioni MSX/TSX supportate.  
  
||**TSX = 7.0**|**TSX = 8.0 &LT; SP3**|**TSX = 8.0 SP3 o versione successiva**|**TSX = 9.0**|**TSX= 10.0**|**TSX = 10.5**|**TSX = 11.0**|  
|-|--------------------|---------------------------|----------------------------------|--------------------|--------------------|---------------------|---------------------|  
|**MSX = 7.0**|Yes|Yes|no|No|No|No|No|  
|**MSX = 8.0 < SP3**|Yes|Yes|No|No|No|No|No|  
|**MSX = 8.0 SP3 o versione successiva**|No|No|Yes|Yes|Yes|Yes|Yes|  
|**MSX = 9.0**|No|no|No|Yes|Yes|Yes|Yes|  
|**MSX = 10.0**|no|no|No|No|Yes|Yes|Yes|  
|**MSX = 10.5**|No|No|No|No|No|Yes|Yes|  
|**MSX = 11.0**|No|No|No|No|No|No|Yes|  
  
 Al momento della creazione di un ambiente multiserver, è opportuno considerare i problemi seguenti:  
  
-   Ogni server di destinazione fa riferimento a un solo server master. Per integrare un server di destinazione in un server master diverso, è necessario escluderlo dal server master corrente.  
  
-   Per modificare il nome di un server di destinazione, è necessario escludere il server, modificarne il nome e quindi reintegrarlo dopo la modifica.  
  
-   Per annullare una configurazione multiserver, è necessario escludere tutti i server di destinazione dal server master.  
  
-   SQL Server Integration Services supporta solo server di destinazione la cui versione è uguale o superiore alla versione del server master.  
  
## <a name="related-tasks"></a>Attività correlate  
 Negli argomenti seguenti vengono illustrate le attività comuni necessarie per la creazione di un ambiente multiserver.  
  
|Descrizione|Argomento|  
|-----------------|-----------|  
|Viene illustrato come creare un server master.|[Configurare un server master](make-a-master-server.md)|  
|Viene illustrato come creare un server di destinazione.|[Configurare un server di destinazione](make-a-target-server.md)|  
|Viene illustrato come integrare un server di destinazione in un server master.|[Integrare un server di destinazione in un server master](enlist-a-target-server-to-a-master-server.md)|  
|Viene illustrato come escludere un server di destinazione da un server master.|[Escludere un server di destinazione da un server master](defect-a-target-server-from-a-master-server.md)|  
|Viene illustrato come escludere più server di destinazione da un server master.|[Escludere più server di destinazione da un server master](defect-multiple-target-servers-from-a-master-server.md)|  
|Viene illustrato come verificare lo stato di un server di destinazione.|[sp_help_targetserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)<br /><br /> [sp_help_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)|  
  
## <a name="see-also"></a>Vedere anche  
 [Risolvere i problemi relativi a processi multiserver che usano proxy](troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
  
