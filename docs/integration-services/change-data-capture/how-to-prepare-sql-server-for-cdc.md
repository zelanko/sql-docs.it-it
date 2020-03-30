---
title: Procedura di preparazione di SQL Server per CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f13e8eae235eb040e92baa15247b6094e9aa1075
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294697"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>Procedura di preparazione di SQL Server per CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Il servizio Oracle CDC richiede che tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione contengano il database MSXDBCDC. Questo database viene creato utilizzando l'azione Prepare SQL Server in CDC Service Configuration Console. Questa attività viene effettuata una sola volta per ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 Di seguito viene illustrato come preparare un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per Change Data Capture Oracle utilizzando CDC Service Configuration Console. Tramite questo processo viene creato il database MSXDBCDC e vengono definite le tabelle, le stored procedure e altri artefatti obbligatori.  
  
 La preparazione di SQL Server per Oracle CDC viene effettuata dall'amministratore del servizio Oracle CDC. Per ulteriori informazioni sul ruolo di amministratore del servizio CDC, vedere [User Roles](../../integration-services/change-data-capture/user-roles.md).  
  
### <a name="to-enable-sql-server-for-cdc"></a>Per abilitare SQL Server per CDC  
  
1.  Dal menu **Start** , selezionare **CDC Service Configuration for Oracle**.  
  
2.  Dal riquadro sinistro selezionare **Local CDC Services** , quindi dal riquadro **Actions** fare clic su **Prepare SQL Server**.  
  
     È anche possibile fare clic con il pulsante destro del mouse su **Local CDC Services** e scegliere **Prepare SQL Server**.  
  
3.  Immettere le informazioni obbligatorie nella finestra di dialogo Preparing SQL Server Instance for Oracle CDC. Per informazioni sull'immissione delle informazioni obbligatorie in questa finestra di dialogo, vedere [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md).  
  
     Per preparare l'istanza di SQL Server per Oracle CDC, l'account di accesso deve disporre di autorizzazioni di scrittura per il database MSXDBCDC. Immettere le credenziali per un account di accesso che dispone di autorizzazioni per il database MSXDBCDC, ad esempio un membro del ruolo `sysasmin` .  
  
 **Nota**: è possibile fare clic su **View Script** per visualizzare una versione di sola lettura dello script di impostazione. Se necessario, un amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può copiare questo script nella console di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per modificarlo ed eseguirlo.  
  
## <a name="see-also"></a>Vedere anche  
 [Preparare SQL Server per CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
