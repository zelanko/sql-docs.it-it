---
title: Provider WMI per eventi del Server classi e proprietà | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eaa82b6f8b7f4a1abc8e43e16eee87ad2513bdb1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039192"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>Classi e proprietà del provider WMI per eventi del server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Gli eventi del server seguenti costituiscono il modello di programmazione per il provider WMI per eventi del server. Esistono due principali categorie di eventi che è possibile sottoporre a query eseguendo le query WQL sul provider: eventi DDL (Data Definition Language) ed eventi di traccia. Anche gli eventi di Service Broker QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED possono essere sottoposti a query. Si noti la natura inclusiva dei diagrammi ad albero seguenti. L'evento DDL_ASSEMBLY_EVENTS, ad esempio, include un evento ALTER_ASSEMBLY, CREATE_ASSEMBLY e DROP_ASSEMBLY. Allo stesso modo, l'evento TRC_FULL_TEXT include un evento FT_CRAWL_ABORTED, FT_CRAWL_STARTED e FT_CRAWL_STOPPED. ALL_EVENTS include tutti gli eventi DDL, gli eventi di traccia, QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED.  
  
 Per informazioni sulle proprietà che possono essere sottoposte a query da un evento o un gruppo di eventi, fare riferimento allo schema dell'evento. Per impostazione predefinita, lo schema degli eventi viene installato nella directory seguente: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
 In alternativa, è possibile fare riferimento allo schema dell'evento pubblicato [ https://schemas.microsoft.com/sqlserver ](https://go.microsoft.com/fwlink/?linkid=43100).  
  
 Ad esempio, facendo riferimento all'evento ALTER_DATABASE, si apprenderà che il relativo evento padre è DDL_SERVER_LEVEL_EVENTS e le relative proprietà siano **TSQLCommand** e **DatabaseName**. L'evento eredita inoltre le proprietà **SQLInstance**, **PostTime**, **ComputerName**, **SPID**, e **LoginName** . L'evento non dispone di eventi figli.  
  
> [!NOTE]  
>  Le stored procedure di sistema che eseguono operazioni di tipo DDL possono inoltre attivare le notifiche degli eventi. Testare le notifiche degli eventi per determinarne le risposte alle stored procedure di sistema eseguite. Ad esempio, l'istruzione CREATE TYPE e **sp_addtype** stored procedure attivano una notifica degli eventi creata in un evento CREATE_TYPE. Per altre informazioni, vedere[eventi DDL](../../relational-databases/triggers/ddl-events.md).  
  
 **Eventi Data Definition Language e gruppi di eventi**  
  
 ![Provider WMI per la struttura di eventi eventi di Server](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "Provider WMI per la struttura di eventi eventi di Server")  
  
 **Gli eventi di traccia e gruppi di eventi**  
  
 ![Gli eventi e gruppi di eventi di traccia](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "traccia eventi e gruppi di eventi")  
  
## <a name="see-also"></a>Vedere anche  
 [Provider WMI per concetti degli eventi Server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [Utilizzo di WQL con il provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
