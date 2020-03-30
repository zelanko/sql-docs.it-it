---
title: Procedura per l'uso dei servizi CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db5c718a-6e7f-48ec-82a3-9d5b131716e5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9202cf969f87c23af7af7d68b01b4a42cff167d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298705"
---
# <a name="how-to-work-with-cdc-services"></a>Procedura di utilizzo dei servizi CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In questa procedura viene descritto come utilizzare CDC Service Configuration Console per preparare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare con i servizi Oracle CDC e creare un nuovo servizio CDC.  
  
### <a name="to-work-with-cdc-services"></a>Per utilizzare i servizi CDC  
  
1.  Dal menu **Start** , selezionare **CDC Service Configuration for Oracle**.  
  
2.  Dal riquadro sinistro selezionare **Local CDC Services** (livello radice).  
  
3.  Viene eseguita una delle attività seguenti o entrambe:  
  
    -   **Prepare SQL Server**  
  
         Selezionare questa opzione dal riquadro **Actions** sul lato destro di CDC Service Configuration Console.  
  
         È anche possibile fare clic con il pulsante destro del mouse su **Local CDC Services** e scegliere **Prepare SQL Server**.  
  
         Verrà visualizzata la finestra di dialogo Preparing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instance for Oracle CDC.  
  
         Per preparare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i servizi Oracle CDC, l'account di accesso deve disporre di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il ruolo predefinito del server `dbcreator` . Questo account di accesso viene utilizzato per creare il database MSXDBCDC obbligatorio per l'aggiunta di servizi Oracle CDC e, successivamente, di istanze di Oracle CDC.  
  
         Per informazioni su come utilizzare questa finestra di dialogo, vedere [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md). Per informazioni su come abilitare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per CDC, vedere [Procedura di preparazione di SQL Server per CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md).  
  
    -   **Creare un nuovo servizio CDC**  
  
         Fare clic su **New Service** dal riquadro **Actions** sul lato destro di CDC Service Configuration Console.  
  
         È anche possibile fare clic con il pulsante destro del mouse su **Local CDC Services** e scegliere **New Service**.  
  
         Verrà aperta la finestra di dialogo New Oracle CDC Service.  
  
         Per informazioni su come utilizzare questa finestra di dialogo, vedere [Creare e modificare un servizio Oracle CDC](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md). Per informazioni sulla procedura di creazione o modifica di un servizio CDC, vedere [Procedura di creazione e modifica di un servizio CDC](../../integration-services/change-data-capture/how-to-create-and-edit-a-cdc-service.md).  
  
         È sufficiente che l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato dal servizio Oracle CDC sia membro del ruolo predefinito del server `public` , non sono necessari altri privilegi. Tuttavia, per creare il servizio Oracle CDC, l'account di accesso deve avere l'autorizzazione di scrittura per il database MSXDBCDC, ad esempio è necessario che all'account di accesso sia assegnato il ruolo del database **db_owner** . Quando si tenta di creare una nuova istanza di Oracle CDC da un account di accesso senza autorizzazione di scrittura per il database MSXDBDCDC, viene visualizzato un messaggio di errore. Fare clic su **OK** nella finestra di dialogo per visualizzare la finestra di dialogo Connect to SQL Server.  
  
         Per informazioni su come immettere le credenziali per un account di accesso che ha l'autorizzazione di scrittura per il database MSXDBCDC, ad esempio il ruolo del database **db_owner** , vedere [Creare e modificare un servizio Oracle CDC](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) e [Connessione a SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i servizi CDC](../../integration-services/change-data-capture/work-with-cdc-services.md)  
  
  
