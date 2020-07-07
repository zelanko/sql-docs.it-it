---
title: File e numeri di versione | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d682ca3d6768da16d43c3c09471a6c722561dd3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008625"
---
# <a name="files-and-version-numbers"></a>File e numeri di versione
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Tutti i componenti SMO (SQL Server Management Object) necessari sono inclusi nel pacchetto NuGet Microsoft. SqlServer. SqlManagementObjects. SMO viene implementato in diversi assembly gestiti. È possibile sviluppare applicazioni SMO in un client o in un server.  

> > [!Important]
> > La versione del file degli assembly SMO viene visualizzata come principale. **0**. Build. Revision. La versione dell'assembly incorporato è però principale. **100**. Build. Revision. Questa operazione viene eseguita per garantire che la versione di SMO utilizzata in ogni applicazione sia separata, in modo che gli aggiornamenti a uno non influiscano su altri.
> > 
> > Per questo motivo, è consigliabile **non** installare queste versioni degli assembly nella global assembly cache (GAC). Questa operazione potrebbe causare l'interruzioni di altre applicazioni, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio. 
  
|File|Descrizione|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Contiene supporto per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contiene supporto per la programmazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. È richiesto solo in programmi che accedono a Service Broker.|  
|Microsoft.SqlServer.Smo.dll|Contiene la maggior parte delle classi SMO.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contiene il supporto per le classi SMO.|  
|Microsoft.SqlServer.WmiEnum.dll|Contiene le classi del provider Strumentazione gestione Windows (WMI, Windows Management Instrumentation). È richiesto solo per programmi che utilizzano le classi del Provider WMI.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Contiene le classi del server registrato. È richiesto solo per programmi che utilizzano le classi del server registrato.|  
  
  
