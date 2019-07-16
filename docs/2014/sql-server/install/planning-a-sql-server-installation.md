---
title: Pianificazione di un'installazione di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1baf29a88ff25eb278271719680d1979940c590
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211490"
---
# <a name="planning-a-sql-server-installation"></a>Pianificazione di un'installazione di SQL Server
  Per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], effettuare le operazioni seguenti:  
  
-   Esaminare i requisiti di installazione, i controlli di configurazione del sistema e le considerazioni sulla sicurezza per un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per installare o eseguire l'aggiornamento a una versione successiva.  
  
-   Utilizzare le utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Indipendentemente dal metodo di installazione, è necessario confermare l'accettazione delle condizioni di licenza del software come utente singolo o per conto di un'entità, a meno che l'utilizzo del software non sia disciplinato da un contratto separato, ad esempio un contratto multilicenza [!INCLUDE[msCoName](../../includes/msconame-md.md)] o un contratto di terze parti con un fornitore di software indipendente o un OEM.  
  
 Le condizioni di licenza vengono visualizzate per la revisione e l'accettazione nell'interfaccia utente del programma di installazione. Le installazioni automatiche che utilizzano i parametri /Q o /QS devono includere il parametro /IAcceptSQLServerLicenseTerms. È possibile esaminare separatamente le condizioni di licenza alla pagina [Condizioni di Licenza Microsoft](https://go.microsoft.com/fwlink/?LinkID=148209).  
  
> [!NOTE]  
>  A seconda della modalità di ricezione del software, ad esempio attraverso un contratto multilicenza [!INCLUDE[msCoName](../../includes/msconame-md.md)] , l'utilizzo del software potrebbe essere soggetto a condizioni aggiuntive.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Novità relative all'installazione di SQL Server](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)  
 In questo argomento vengono descritti i dettagli sulle caratteristiche di installazione nuove o migliorate disponibili in questa versione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Requisiti hardware e software per l'installazione di SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
 In questo argomento vengono elencati i requisiti hardware e software minimi per l'installazione e l'esecuzione di un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 Questo argomento illustra alcune procedure consigliate per la sicurezza, da prendere in considerazione prima dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dopo l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 Nel presente argomento viene fornita la descrizione della configurazione predefinita dei servizi disponibili in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e delle opzioni di configurazione per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile impostare durante e dopo l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [Protocolli e librerie di rete](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)  
 In questo argomento viene fornita la descrizione della configurazione predefinita dei protocolli di rete disponibili questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e delle opzioni di configurazione disponibili.  
  
 [Utilizzare più versioni e istanze di SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 In questo argomento sono contenute le considerazioni relative alle installazioni di più versioni e istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Versioni in lingua locale di SQL Server](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
 In questo argomento vengono descritte le versioni localizzate di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Installare SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
 In questa sezione è contenuta una panoramica delle diverse opzioni disponibili per l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Installare le funzionalità di Business Intelligence di SQL Server 2014](install-sql-server-business-intelligence-features.md)  
 In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene illustrata la modalità di installazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che fanno parte della piattaforma di Business Intelligence di Microsoft.  
  
 [Aggiornamento a SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)  
 Nella sezione vengono forniti cenni preliminari sull'aggiornamento delle istanze delle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Disinstallare SQL Server 2014](uninstall-sql-server.md)  
 Fare riferimento a questa sezione per disinstallare completamente un'istanza esistente di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e preparare il sistema in modo che sia possibile reinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Installazione del cluster di failover di SQL Server](../failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono descritte le modalità di installazione e configurazione del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio rapido di installazione di SQL Server 2014](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)   
 [Installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../failover-clusters/high-availability-solutions-sql-server.md)   
 [Operazioni preliminari all'installazione del clustering di failover](../failover-clusters/install/before-installing-failover-clustering.md)   
 [Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata di &#40;programma di installazione&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
