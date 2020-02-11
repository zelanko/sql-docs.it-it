---
title: Bilanciamento del carico dei pacchetti su server remoti tramite SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- load-balancing [Integration Services]
- parent packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7c1f4792d97ae82561f0d05fe9754daae0a2bf3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62890171"
---
# <a name="load-balancing-packages-on-remote-servers-by-using-sql-server-agent"></a>Bilanciamento del carico dei pacchetti su server remoti tramite SQL Server Agent
  Quando è necessario eseguire numerosi pacchetti, è preferibile utilizzare altri server eventualmente disponibili. L'utilizzo di altri server per l'esecuzione di più pacchetti controllati da un unico pacchetto padre è detto bilanciamento del carico. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]il bilanciamento del carico è una procedura manuale che deve essere progettata dai proprietari dei pacchetti. Il bilanciamento del carico non viene infatti eseguito automaticamente dai server. Inoltre, sui server remoti è possibile eseguire esclusivamente pacchetti interi, non singole attività in altri pacchetti.  
  
 Il bilanciamento del carico risulta utile negli scenari seguenti:  
  
-   I pacchetti possono essere eseguiti contemporaneamente.  
  
-   I pacchetti sono di grandi dimensioni e, se eseguiti sequenzialmente, richiedere un tempo di esecuzione superiore al tempo massimo consentito per l'elaborazione.  
  
 Amministratori e architetti possono stabilire se l'utilizzo di server aggiuntivi per l'elaborazione può costituire un vantaggio per i processi.  
  
## <a name="illustration-of-load-balancing"></a>Illustrazione del bilanciamento del carico  
 Nella figura seguente viene illustrato un pacchetto padre in un server. Il pacchetto padre contiene più attività Esegui processo di SQL Server Agent e ogni attività nel pacchetto padre chiama un processo di SQL Server Agent su un server remoto. Ogni server remoto contiene un processo di SQL Server Agent che include un passaggio in cui viene chiamato un pacchetto su tale server.  
  
 ![Panoramica dell'architettura di bilanciamento del carico di SSIS](../media/loadbalancingoverview.gif "Panoramica dell'architettura di bilanciamento del carico di SSIS")  
  
 I passaggi necessari per il bilanciamento del carico in questa architettura non sono concetti nuovi. Il bilanciamento del carico viene infatti ottenuto utilizzando in modo nuovo concetti esistenti e oggetti SSIS comuni.  
  
## <a name="execution-of-packages-on-a-remote-instance-by-using-sql-server-agent"></a>Esecuzione di pacchetti in un'istanza remota tramite SQL Server Agent  
 Nell'architettura di base per l'esecuzione di pacchetti remoti è presente un pacchetto centrale che risiede nell'istanza di SQL Server che controlla gli altri pacchetti remoti. Tale pacchetto è illustrato nella figura, con il nome Pacchetto SSIS padre. L'istanza in cui risiede tale pacchetto controlla l'esecuzione dei processi di SQL Server Agent che eseguono i pacchetti figlio. I pacchetti figlio non vengono eseguiti in base a una pianificazione fissa controllata da SQL Server Agent sul server remoto, ma vengono avviati da SQL Server Agent quando quest'ultimo viene chiamato dal pacchetto padre e vengono eseguiti nella stessa istanza di SQL Server in cui risiede SQL Server Agent.  
  
 Per poter eseguire un pacchetto remoto tramite SQL Server Agent, è necessario configurare i pacchetti padre e figlio, quindi configurare i processi di SQL Server Agent che controllano i pacchetti figlio. Nelle sezioni seguenti vengono fornite ulteriori informazioni sulle procedure per la creazione, la configurazione, l'esecuzione e la manutenzione di pacchetti eseguiti su server remoti. Il processo include numerosi passaggi:  
  
-   Creazione dei pacchetti figlio e installazione di questi ultimi nei server remoti.  
  
-   Creazione dei processi di SQL Server Agent sulle istanze remote in cui verranno eseguiti i pacchetti.  
  
-   Creazione del pacchetto padre.  
  
-   Determinazione dello scenario di registrazione per i pacchetti figlio.  
  
 Nella tabella seguente vengono forniti i collegamenti agli argomenti che illustrano i passaggi del processo.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Implementazione di pacchetti figlio](../implementation-of-child-packages.md)|Vengono descritte l'installazione dei pacchetti e la creazione dei processi di SQL Server Agent per l'esecuzione di tali pacchetti.|  
|[Implementazione del pacchetto padre](../implementation-of-the-parent-package.md)|Viene descritta la creazione di un pacchetto padre contenente più attività Esegui processo di SQL Server Agent. Ogni attività esegue uno dei pacchetti figlio.|  
|[Registrazione per pacchetti con bilanciamento del carico in server remoti](../logging-for-load-balanced-packages-on-remote-servers.md)|Viene descritto lo scenario di registrazione per i pacchetti remoti.|  
  
## <a name="related-tasks"></a>Attività correlate  
 [Pianificare un pacchetto tramite SQL Server Agent](../schedule-a-package-by-using-sql-server-agent.md)  
  
  
