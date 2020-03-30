---
title: Procedura di gestione di un servizio CDC locale | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 722db3a272c99ba6733551f4fa1a4131971e2416
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298741"
---
# <a name="how-to-manage-a-local-cdc-service"></a>Procedura di gestione di un servizio CDC locale

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In questa procedura viene illustrato come utilizzare CDC Service Configuration Console per gestire servizi CDC specifici.  
  
### <a name="to-manage-a-specific-cdc-service"></a>Per gestire un servizio CDC specifico  
  
1.  Dal menu **Start** , selezionare **CDC Service Configuration for Oracle**.  
  
2.  Dal riquadro sinistro di CDC Service Configuration Console, espandere **Local CDC Services**.  
  
3.  Selezionare il servizio CDC che si desidera utilizzare.  
  
     È inoltre possibile fare clic con il pulsante destro del mouse sul servizio CDC da utilizzare e selezionare l'azione desiderata.  
  
     **OR**  
  
     Selezionare **Local CDC Services** dal riquadro sinistro di CDC Service Configuration Console, quindi selezionare quindi il servizio che si desidera utilizzare dalla sezione centrale della console di configurazione del servizio CDC.  
  
     È inoltre possibile fare clic con il pulsante destro del mouse sul servizio CDC da utilizzare e selezionare l'azione desiderata.  
  
4.  Quando si utilizza un servizio CDC è possibile eseguire le attività seguenti:  
  
    -   **Eliminare il servizio**  
  
         Dal riquadro **Actions** sul lato destro di CDC Service Configuration Console, fare clic su **Delete** per eliminare il servizio.  
  
         È inoltre possibile fare clic con il pulsante destro del mouse sul servizio CDC da eliminare e scegliere **Delete**.  
  
         **Nota**: se il servizio è in esecuzione al momento dell'eliminazione, il servizio viene arrestato prima di essere eliminato.  
  
         Per eliminare una definizione del servizio Windows di Oracle CDC, è necessario aggiornare l'accesso al database MSXDBCDC nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata. Quando si fa clic su **OK** per eliminare il servizio, viene effettuato un tentativo di eliminare la registrazione del servizio Oracle CDC nel database MSXDBCDC. Se l'operazione ha esito negativo a causa della mancanza di autorizzazioni, verrà visualizzata una finestra di dialogo in cui viene richiesto all'utente di immettere un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un accesso di aggiornamento al database MSXDBCDC.  
  
         Per informazioni sui dati da immettere nella finestra di dialogo Connect to SQL Server, vedere [Manage an Oracle CDC Service](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md) e [Connection to SQL Server for Delete](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md).  
  
    -   **Modificare le proprietà del servizio CDC**  
  
         Dal riquadro **Actions** sul lato destro di CDC Service Configuration Console, fare clic su **Properties**.  
  
         È inoltre possibile fare clic con il pulsante destro del mouse sul servizio CDC in cui si desidera modificare le proprietà e scegliere **Properties**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire un servizio Oracle CDC](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  
