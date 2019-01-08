---
title: Impostare un avviso del database di SQL Server (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3342af1de84e922ce63848c8fdffe5aa30ec309a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797034"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Impostazione di un avviso del database di SQL Server (Windows)
  Tramite Monitoraggio di sistema è possibile creare un avviso da generare quando viene raggiunto un valore soglia per un contatore di Monitoraggio di sistema. In risposta all'avviso, Monitoraggio di sistema può avviare un'applicazione, ad esempio un'applicazione personalizzata programmata per gestire la condizione dell'avviso. Ad esempio, è possibile creare un avviso che viene generato quando il numero di deadlock supera un valore specifico.  
  
 È inoltre possibile impostare gli avvisi tramite Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni, vedere [Avvisi](../../ssms/agent/alerts.md).  
  
### <a name="to-set-up-a-sql-server-database-alert"></a>Per impostare un avviso del database di SQL Server  
  
1.  Nell'albero di navigazione della finestra Prestazioni espandere **Avvisi e registri di prestazioni**.  
  
2.  Fare clic con il pulsante destro del mouse su **Avvisi**e quindi scegliere **Impostazioni nuovo avviso**.  
  
3.  Nella finestra di dialogo **Impostazioni nuovo avviso** digitare un nome per il nuovo avviso e quindi fare clic su **OK**.  
  
4.  Nella scheda **Generale** della finestra di dialogo relativa al nuovo avviso inserire un commento nel campo **Commento**e fare clic su **Aggiungi** per aggiungere un contatore all'avviso.  
  
     Tutti gli avvisi devono avere almeno un contatore.  
  
5.  Nella finestra di dialogo Aggiungi contatori selezionare un oggetto di SQL Server nell'elenco **Oggetto prestazione** e quindi selezionare un contatore in **Seleziona i contatori dall'elenco**.  
  
6.  Per aggiungere il contatore all'avviso, fare clic su **Aggiungi**. È possibile continuare ad aggiungere contatori oppure fare clic su **Chiudi** per tornare alla finestra di dialogo del nuovo avviso.  
  
7.  Nella finestra di dialogo del nuovo avviso selezionare **Superiore** o **Inferiore**nell'elenco **Avvisa quando il valore è** e quindi specificare un valore soglia in **Limite**.  
  
     L'avviso viene generato quando il valore del contatore è superiore o inferiore al valore soglia, a seconda che sia stato selezionato **Superiore** o **Inferiore**.  
  
8.  Nelle caselle **Campiona dati ogni** impostare la frequenza di campionamento.  
  
9. Nella scheda **Azione** impostare le azioni in modo che vengano eseguite ogni volta che viene generato l'avviso.  
  
10. Nella scheda **Pianificazione** impostare l'avvio e l'arresto pianificati per l'analisi dell'avviso.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un avviso del database di SQL Server](../performance-monitor/create-a-sql-server-database-alert.md)  
  
  
