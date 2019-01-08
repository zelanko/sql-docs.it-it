---
title: Impostare un'istanza di SQL Server per l'avvio automatico (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 300b539e132b9bda9bc6540c0aadcac6ab9f11a1
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640313"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>Impostare un'istanza di SQL Server per l'avvio automatico (Gestione configurazione SQL Server)
  In questo argomento viene illustrato come impostare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'avvio automatico in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando Gestione configurazione SQL Server. Durante l'installazione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene normalmente configurato per l'avvio automatico. In caso contrario, è possibile modificare questa impostazione in qualsiasi momento.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>Per impostare un'istanza di SQL Server per l'avvio automatico  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
    > [!NOTE]  
    >  Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle nuove versioni di Windows.  
    >   
    >  -   **Windows 10**:  
    >          Per aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, via il **pagina iniziale**, digitare SQLServerManager12.msc (per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sostituire 12 con un numero inferiore. Facendo clic su SQLServerManager12.msc apre Gestione configurazione. Per aggiungere Gestione configurazione alla pagina iniziale o alla barra delle applicazioni, fare doppio clic su SQLServerManager12.msc e quindi fare clic su **Apri percorso file**. In Esplora File di Windows, fare doppio clic su SQLServerManager12.msc e quindi fare clic su **Aggiungi a Start** oppure **Pin alla barra delle applicazioni**.  
    > -   **Windows 8**:  
    >          Per aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, nel **ricerca** sull'accesso, in **app**, digitare **SQLServerManager\<versione >. msc** , ad esempio `SQLServerManager12.msc`, quindi premere **invio**.  
  
2.  In **Gestione configurazione SQL Server**espandere **Servizi**e quindi fare clic su **SQL Server**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sul nome dell'istanza per la quale impostare l'avvio automatico, quindi scegliere **Proprietà**.  
  
4.  Nella finestra di dialogo **SQL Server \<***nomeistanza***> Proprietà** impostare  **Modalità di avvio** su **Automatica**.  
  
5.  Fare clic su **OK**e chiudere Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Impedire l'avvio automatico di un'istanza di SQL Server &#40;Gestione configurazione SQL Server&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Connettersi a un altro computer &#40;Gestione configurazione SQL Server&#41;](scm-services-connect-to-another-computer.md)   
 [Configurazione di WMI per mostrare lo stato del server in Strumenti SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
