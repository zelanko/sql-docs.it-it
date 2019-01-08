---
title: Modello a oggetti SMO | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 637c60fd6d7ba53087a145135d7152066983b644
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808593"
---
# <a name="smo-object-model"></a>Modello a oggetti SMO
  Il modello a oggetti SMO è costituito da una gerarchia di oggetti. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> rappresenta l'oggetto di livello principale e tutti gli oggetti classe di istanza si trovano all'interno dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
 La classe <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> è una classe di livello principale con una gerarchia di oggetti distinta. Il <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> oggetto rappresenta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizi e le impostazioni di rete disponibili tramite il Provider WMI.  
  
 Oltre agli oggetti <xref:Microsoft.SqlServer.Management.Smo.Server> e <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>, sono disponibili diverse classi di utilità che rappresentano attività e operazioni, ad esempio <xref:Microsoft.SqlServer.Management.Smo.Transfer>, <xref:Microsoft.SqlServer.Management.Smo.Backup> o <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
 Il modello a oggetti SMO è costituito da diversi spazi dei nomi. Per altre informazioni, vedere [Spazio dei nomi SMO](smo-object-model-namespaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Diagramma del modello a oggetti SMO](smo-object-model-diagram.md)   
 [Spazi dei nomi SMO](smo-object-model-namespaces.md)   
 [Concetti relativi al provider WMI per Gestione configurazione](../wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
