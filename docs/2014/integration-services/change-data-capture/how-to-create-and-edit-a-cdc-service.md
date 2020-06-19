---
title: Procedura di creazione e modifica di un servizio CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9b01b0f92be08b86f8cbcd2ec6405ffdc8b4eee8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84923162"
---
# <a name="how-to-create-and-edit-a-cdc-service"></a>Procedura di creazione e modifica di un servizio CDC
  In queste procedure viene illustrato come creare e modificare un nuovo servizio Oracle CDC da CDC Service Configuration Console.  
  
 Per questa procedura è necessario un utente di Windows con privilegi di amministratore per il computer in cui viene configurato il servizio Oracle CDC.  
  
### <a name="to-create-a-new-cdc-service"></a>Per creare un nuovo servizio CDC  
  
1.  Dal menu **Start** , selezionare **CDC Service Configuration for Oracle**.  
  
2.  Dal riquadro sinistro fare clic con il pulsante destro del mouse su Local CDC Services e selezionare New Service.  
  
     È inoltre possibile fare clic su **New Service** nel riquadro **Actions** .  
  
3.  Digitare o immettere le informazioni richieste nella finestra di dialogo New Oracle CDC Service. Per informazioni sull'immissione di informazioni nella finestra di dialogo New Oracle CDC Service, vedere [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md) .  
  
     L'account di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornito nella finestra di dialogo New Oracle CDC Service viene utilizzato dal servizio Oracle CDC per l'esecuzione. È sufficiente che l'account di accesso sia membro del ruolo predefinito del server pubblico, non sono necessari altri privilegi. Una volta aggiunte nuove istanze di Oracle CDC, l'account di accesso riceve l'accesso **db_owner** ai database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC associati.  
  
4.  Al termine dell'immissione delle informazioni necessarie, fare clic su **OK**.  
  
     Per creare la definizione del servizio Windows di Oracle CDC, è necessario aggiornare l'accesso al database MSXDBCDC nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata. Quando si fa clic su **OK**, una finestra di dialogo richiede all'utente di immettere un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un accesso aggiornato al database MSXDBCDC.  
  
     Per informazioni sui dati da digitare nella finestra di dialogo Connect to SQL Server, vedere [Connection to SQL Server](connection-to-sql-server.md).  
  
5.  Scegliere **OK** per chiudere la finestra di dialogo New Oracle CDC Service.  
  
### <a name="to-edit-a-cdc-service"></a>Per modificare un servizio CDC  
  
1.  Dal menu **Start** , selezionare **CDC Service Configuration for Oracle**.  
  
2.  Dal riquadro sinistro selezionare **Local CDC Services** (Servizi CDC locali) e quindi fare clic con il pulsante destro del mouse sul servizio locale da modificare e selezionare **Properties**(Proprietà).  
  
     È inoltre possibile selezionare il servizio utilizzato al centro, quindi nel riquadro **Actions** fare clic su **Properties**.  
  
3.  Digitare o immettere le informazioni richieste nella finestra di dialogo CDC Service Properties. Per informazioni sull'immissione di informazioni nella finestra di dialogo CDC Service Properties, vedere [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md) .  
  
4.  Al termine dell'immissione delle informazioni richieste, fare clic su **OK**. Verrà visualizzata la finestra di dialogo Connect to SQL Server.  
  
     Quando si tenta di creare una nuova istanza di Oracle CDC da un account di accesso senza autorizzazione di scrittura per il database MSXDBDCDC, viene visualizzato un messaggio di errore. Fare clic su **OK** nella finestra di dialogo per visualizzare la finestra di dialogo Connect to SQL Server. In questa finestra di dialogo è necessario immettere le credenziali per un account di accesso con autorizzazione di scrittura per il database MSXDBCDC, ad esempio il ruolo del database **db_owner** .  
  
     Per informazioni sui dati da digitare nella finestra di dialogo Connect to SQL Server, vedere [Connection to SQL Server](connection-to-sql-server.md).  
  
5.  Fare clic su **OK** nella finestra di dialogo Connect to Oracle. Verranno chiuse entrambe le finestre di dialogo e il servizio verrà aggiornato e registrato.  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione Change Data Capture per Oracle di Attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Creare e modificare un servizio Oracle CDC](create-and-edit-an-oracle-cdc-service.md)  
  
  
