---
title: Abilitare un server di pubblicazione remoto in un database di distribuzione (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7b554dc39832a834ebe1bc2ac2d4bfefa21721a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721313"
---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>Abilitazione di un server di pubblicazione remoto in un database di distribuzione (SQL Server Management Studio)
  Attivare un server di pubblicazione per l'utilizzo di un server di distribuzione remoto nella pagina **Server di pubblicazione** . Questa pagina è disponibile nella Configurazione guidata distribuzione e nella finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md) e [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>Per attivare un server di pubblicazione nella Configurazione guidata distribuzione  
  
1.  Nella pagina **Server di pubblicazione** della Configurazione guidata distribuzione fare clic su **Aggiungi**.  
  
2.  Fare clic su **Aggiungi server di pubblicazione SQL Server**. Per informazioni sull'attivazione di un server di pubblicazione Oracle per l'utilizzo di un server di distribuzione, vedere [Create a Publication from an Oracle Database](publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Nella finestra di dialogo **Connetti al server** specificare le informazioni sulla connessione del server di pubblicazione che utilizzerà il server di distribuzione remoto e fare clic su **Connetti**.  
  
4.  Nelle caselle di testo **Password** e **Conferma password** della pagina **Password server di distribuzione** specificare una password complessa per l'account **distributor_admin** , che verrà utilizzata durante la replica per la connessione dal server di pubblicazione al server di distribuzione allo scopo di eseguire le attività amministrative.  
  
5.  Per visualizzare e modificare le impostazioni relative a un server di pubblicazione, fare clic sul pulsante delle proprietà ( **...** ).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>Per abilitare un server di pubblicazione nella finestra di dialogo Proprietà database di distribuzione  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** fare clic su **Aggiungi**.  
  
2.  Fare clic su **Aggiungi server di pubblicazione SQL Server**. Per informazioni sull'attivazione di un server di pubblicazione Oracle per l'utilizzo di un server di distribuzione, vedere [Create a Publication from an Oracle Database](publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Nella finestra di dialogo **Connetti al server** specificare le informazioni sulla connessione del server di pubblicazione che utilizzerà il server di distribuzione remoto e fare clic su **Connetti**.  
  
4.  Nelle caselle di testo **Password** e **Conferma password** della pagina **Server di pubblicazione** specificare una password complessa per l'account **distributor_admin** , che verrà utilizzata durante la replica per la connessione dal server di pubblicazione al server di distribuzione allo scopo di eseguire le attività amministrative.  
  
5.  Per visualizzare e modificare le impostazioni relative a un server di pubblicazione, fare clic sul pulsante delle proprietà ( **...** ).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md)   
 [Configura distribuzione](configure-distribution.md)   
 [Proteggere il database di distribuzione](security/secure-the-distributor.md)  
  
  
