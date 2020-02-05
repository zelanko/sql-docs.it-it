---
title: Impedire l'avvio automatico di un'istanza di SQL Server (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4293a8595ed287219da6e0d2f23e907236456daf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68025660"
---
# <a name="scm-services---prevent-automatic-startup-of-an-instance"></a>Impedire l'avvio automatico di un'istanza di SQL Server (Gestione configurazione SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come impedire che un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga avviata automaticamente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando Gestione configurazione SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è normalmente configurato per l'avvio automatico. È possibile modificare questa configurazione impostando su manuale la modalità di avvio per l'istanza.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>Per impedire l'avvio automatico di un'istanza di SQL Server  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
    > [!NOTE]  
    >  Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle versioni più recenti di Windows.  
    >   
    >  -   **Windows 10**:  
    >          per aprire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nella **pagina iniziale**digitare SQLServerManager13.msc (per [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sostituire 13 con un numero inferiore. Se si fa clic su SQLServerManager13.msc, viene aperto Gestione configurazione. Per aggiungere Gestione configurazione alla pagina iniziale o alla barra delle applicazioni, fare clic con il pulsante destro del mouse su SQLServerManager13.msc e quindi scegliere **Apri percorso file**. In Esplora file di Windows fare clic con il pulsante destro del mouse su SQLServerManager13.msc e quindi scegliere **Aggiungi a Start** o **Aggiungi alla barra delle applicazioni**.  
    > -   **Windows 8**:  
    >          Per aprire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nell'accesso alla **ricerca** in **App** digitare **SQLServerManager\<versione>.msc**, ad esempio **SQLServerManager13.msc** e quindi premere **INVIO**.  
  
2.  In Gestione configurazione SQL Server espandere **Servizi**e quindi fare clic su **SQL Server**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **MSSQLServer**quindi scegliere **Proprietà**.  
  
4.  Nella finestra di dialogo **SQL Server \<** _nomeistanza_ **> Proprietà** nella scheda **Servizio** della casella **Generale** impostare il valore di **Modalità di avvio** su **Manuale**.  
  
5.  Fare clic su **OK** per chiudere la finestra di dialogo**SQL Server \<** _nomeistanza_ **> Proprietà** e quindi chiudere Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
