---
title: Classi e proprietà del provider WMI per eventi del server
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
ms.openlocfilehash: 08b18a3a5805b37a371d6fa17850584d6f4953fd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74164914"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>Classi e proprietà del provider WMI per eventi del server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Gli eventi del server seguenti costituiscono il modello di programmazione per il provider WMI per eventi del server. Esistono due principali categorie di eventi che è possibile sottoporre a query eseguendo le query WQL sul provider: eventi DDL (Data Definition Language) ed eventi di traccia. Anche gli eventi di Service Broker QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED possono essere sottoposti a query. Si noti la natura inclusiva dei diagrammi ad albero seguenti. L'evento DDL_ASSEMBLY_EVENTS, ad esempio, include un evento ALTER_ASSEMBLY, CREATE_ASSEMBLY e DROP_ASSEMBLY. Allo stesso modo, l'evento TRC_FULL_TEXT include un evento FT_CRAWL_ABORTED, FT_CRAWL_STARTED e FT_CRAWL_STOPPED. ALL_EVENTS include tutti gli eventi DDL, gli eventi di traccia, QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED.  
  
 Per informazioni sulle proprietà che possono essere sottoposte a query da un evento o un gruppo di eventi, fare riferimento allo schema dell'evento. Per impostazione predefinita, lo schema dell'evento viene installato nella directory seguente: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
 In alternativa, è possibile fare riferimento allo schema dell'evento pubblicato [https://schemas.microsoft.com/sqlserver](https://go.microsoft.com/fwlink/?linkid=43100)in.  
  
 Se ad esempio si fa riferimento all'evento ALTER_DATABASE, si apprenderà che l'evento padre viene DDL_SERVER_LEVEL_EVENTS e le relative proprietà sono **TSQLCommand** e **DatabaseName**. L'evento eredita inoltre le proprietà **SQLInstance**, **posttime**, **nomecomputer**, **SPID**e **LoginName**. L'evento non dispone di eventi figli.  
  
> [!NOTE]  
>  Le stored procedure di sistema che eseguono operazioni di tipo DDL possono inoltre attivare le notifiche degli eventi. Testare le notifiche degli eventi per determinarne le risposte alle stored procedure di sistema eseguite. Ad esempio, l'istruzione CREATE TYPE e **sp_addtype** stored procedure genereranno una notifica degli eventi creata in un evento di CREATE_TYPE. Per ulteriori informazioni, vedere [eventi DDL](../../relational-databases/triggers/ddl-events.md).  
  
 **Eventi e gruppi di eventi del linguaggio di definizione dei dati**  
  
 ![Albero degli eventi del provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "Albero degli eventi del provider WMI per eventi del server")  
  
 **Eventi e gruppi di eventi di traccia**  
  
 ![Eventi di traccia e gruppi di eventi](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "Eventi di traccia e gruppi di eventi")  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi al provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [Utilizzo di WQL con il provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
