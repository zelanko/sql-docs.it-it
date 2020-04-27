---
title: Stato di preparazione aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 697f70d4435213a991e55adecb51a98120d8df1b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091558"
---
# <a name="upgrade-advisor-progress"></a>Stato Preparazione aggiornamento
  L'analisi di Preparazione aggiornamento inizia con un analizzatore dedicato che esegue un'analisi di ogni componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionato. Quando si analizzano i componenti, lo stato di avanzamento viene segnalato nella finestra di dialogo **stato** .  
  
## <a name="options"></a>Opzioni  
 **Azione**  
 Specifica il componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionato per l'analisi.  
  
 **Stato**  
 Visualizza il valore relativo allo stato restituito dall'interfaccia di avanzamento dei componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Messaggio**  
 Visualizza i messaggi di errore oppure quelli relativi a esito positivo o negativo restituiti dal singolo analizzatore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se l'analisi risulta troppo lenta, è possibile arrestarla, chiudere l'Analisi guidata di Preparazione aggiornamento e quindi eseguire nuovamente la procedura guidata. Per ridurre i tempi di analisi, selezionare un numero minore di componenti da analizzare.  
  
 Al termine dell'analisi, il report viene scritto in un file. È possibile visualizzare il report facendo clic su **Avvia report** per avviare il Visualizzatore di report da questa pagina. Se si desidera visualizzare il report in un secondo momento, è possibile aprire il **Visualizzatore report di preparazione aggiornamento** dalla pagina iniziale di preparazione aggiornamento.  
  
> [!NOTE]  
>  I report precedenti vengono salvati ogni volta che si analizza un server. I report vengono salvati utilizzando il valore timestamp come nome del file. Nel visualizzatore di report vengono visualizzati gli ultimi cinque report salvati.  
  
## <a name="see-also"></a>Vedi anche  
 [Procedura: avvio di preparazione aggiornamento](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Procedura: esecuzione dell'analisi guidata di preparazione aggiornamento](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Componenti SQL Server](../../../2014/sql-server/install/sql-server-components.md)   
 [Guida di riferimento all'interfaccia utente di preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
