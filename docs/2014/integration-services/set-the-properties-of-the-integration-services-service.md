---
title: Impostare le proprietà del servizio Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- Integration Services service, properties
ms.assetid: 3a8ad546-0f58-4b31-ab56-58d6313b1098
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c40ec2d7da7dc8f46644632d29b6fb8d1101ff9b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055643"
---
# <a name="set-the-properties-of-the-integration-services-service"></a>Impostare le proprietà del servizio Integration Services
    
> [!IMPORTANT]  
>  In questo argomento viene illustrato il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servizio Windows per la gestione dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]supporta il servizio per la compatibilità con le versioni precedenti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]di. A partire da [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], è possibile gestire oggetti come i pacchetti del server Integration Services.  
  
 Il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consente di gestire e monitorare i pacchetti in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Quando si installa [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]per la prima [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] volta, il servizio viene avviato e il tipo di avvio del servizio è impostato su automatico.  
  
 Dopo l'installazione del servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è possibile impostare le proprietà del servizio usando Gestione configurazione SQL Server o lo snap-in MMC Servizi.  
  
 Per configurare le altre importanti funzionalità del servizio, inclusi i percorsi in cui vengono memorizzati e gestiti i pacchetti, è necessario modificare il file di configurazione del servizio. Per altre informazioni, vedere [Configurazione del servizio Integration Services &#40;servizio SSIS&#41;](service/integration-services-service-ssis-service.md).  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>Per impostare le proprietà del servizio Integration Services tramite Gestione configurazione SQL Server  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, **Microsoft SQL Server**, **Strumenti di configurazione**e quindi fare clic su **Gestione configurazione SQL Server**.  
  
2.  Nello snap-in **Gestione configurazione SQL Server** individuare **SQL Server Integration Services** nell'elenco dei servizi, fare clic con il pulsante destro del mouse su **SQL Server Integration Services**e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà di SQL Server Integration Services** è possibile eseguire una delle operazioni seguenti:  
  
    -   Fare clic sulla scheda **Connessione** per visualizzare le informazioni di accesso, come il nome dell'account.  
  
    -   Fare clic sulla scheda **Servizio** per visualizzare le informazioni relative al servizio, ad esempio il nome del computer host e per specificare la modalità di avvio del servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
        > [!NOTE]  
        >  Nella scheda **Avanzate** non sono disponibili informazioni relative al servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
4.  Fare clic su **OK**.  
  
5.  Scegliere **Esci** dal menu **File** per chiudere lo snap-in **Gestione configurazione SQL Server** .  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>Per impostare le proprietà del servizio Integration Services tramite i Servizi  
  
1.  Nel **Pannello di controllo**fare clic su **Strumenti di amministrazione**nella visualizzazione classica oppure su **Prestazioni e manutenzione** e quindi su **Strumenti di amministrazione**nella visualizzazione per categorie.  
  
2.  Fare clic su **Servizi**.  
  
3.  Nello snap-in **Servizi** individuare **SQL Server Integration Services** nell'elenco dei servizi, fare clic con il pulsante destro del mouse su **SQL Server Integration Services**e quindi scegliere **Proprietà**.  
  
4.  Nella finestra di dialogo **proprietà SQL Server Integration Services** è possibile eseguire le operazioni seguenti:  
  
    -   Fare clic sulla scheda **generale** . Per abilitare il servizio, selezionare il tipo di avvio manuale o automatico. Per disabilitarlo, nella casella **Tipo di avvio** selezionare Disabilita. Quando si seleziona Disabilita, il servizio non viene arrestato se è in esecuzione.  
  
         Se il servizio è già abilitato, è possibile fare clic su **Arresta** per arrestarlo oppure su **Avvia** per avviarlo.  
  
    -   Fare clic sulla scheda **Accedi** per visualizzare o modificare le informazioni relative all'accesso.  
  
    -   Fare clic sulla scheda **Recupero** per visualizzare le risposte predefinite del computer agli errori del servizio. È possibile modificare queste opzioni in base all'ambiente specifico.  
  
    -   Fare clic sulla scheda **Dipendenze** per visualizzare un elenco dei servizi dipendenti. Il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] non ha alcuna dipendenza.  
  
5.  Fare clic su **OK**.  
  
6.  Facoltativamente, se è stato impostato il tipo di avvio manuale o automatico, è possibile fare clic con il pulsante destro del mouse su **SQL Server Integration Services** e quindi scegliere **Avvia, Arresta o Riavvia**.  
  
7.  Scegliere **Esci** dal menu **File** per chiudere lo snap-in **Servizi** .  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione del servizio Integration Services](../../2014/integration-services/manage-the-integration-services-service.md)  
  
  
