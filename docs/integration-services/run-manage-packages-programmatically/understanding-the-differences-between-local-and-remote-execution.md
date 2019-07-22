---
title: Differenze tra l'esecuzione locale e remota | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 61233900def55fc28627869a134bddaf786f5548
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028444"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>Differenze tra l'esecuzione locale e remota

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Gli sviluppatori e gli amministratori di pacchetti dovrebbero essere consapevoli dell'esistenza di restrizioni in merito a dove può essere eseguito un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Un pacchetto viene eseguito nello stesso computer del programma che lo avvia**. Anche quando un programma carica un pacchetto archiviato in remoto in un altro server, il pacchetto viene eseguito nel computer locale.  
  
-   **È possibile eseguire un pacchetto all'esterno dell'ambiente di sviluppo solo in un computer in cui è installato Integration Services**. Non è possibile eseguire i pacchetti all'esterno di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in un computer client in cui [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non è installato e le condizioni di licenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero non consentire l'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in computer aggiuntivi. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un componente server e non è ridistribuibile a computer client. Per eseguire pacchetti da un computer client, è necessario avviarli in modo da assicurarsi che vengano eseguiti nel server.  
  
 Per ulteriori informazioni sul caricamento e l'esecuzione di un pacchetto salvato, vedere:  
  
-   [Caricamento ed esecuzione di un pacchetto locale a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [Caricamento ed esecuzione di un pacchetto remoto a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 Per ulteriori informazioni sull'esecuzione di un pacchetto e il caricamento del relativo output in un programma personalizzato, vedere:  
  
-   [Caricamento dell'output di un pacchetto locale](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Caricamento ed esecuzione di un pacchetto locale a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Caricamento ed esecuzione di un pacchetto remoto a livello di programmazione](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Caricamento dell'output di un pacchetto locale](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
