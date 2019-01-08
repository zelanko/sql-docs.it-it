---
title: Modifiche di rilievo di SQL Server Reporting Services in SQL Server 2016 | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae42e66047d54b305fef2cb48a9d69c0ebb25a44
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591855"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>Modifiche di rilievo di SQL Server Reporting Services in SQL Server 2016

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

In questo argomento vengono descritte le modifiche di rilievo introdotte in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Tali modifiche potrebbero interrompere il funzionamento di applicazioni, funzionalità o script basati su versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. I problemi potrebbero verificarsi durante un aggiornamento oppure in script o report personalizzati.

## <a name="security-extensions"></a>Estensioni di sicurezza

Le estensioni di sicurezza personalizzate richiedono alcune modifiche per funzionare con il nuovo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Le estensioni di sicurezza devono usare l'interfaccia IAuthenticationExtension2.

## <a name="wmi-provider"></a>Provider WMI

Il nome dell'applicazione [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] cambia da "ReportManager" a "ReportServerWebApp".

## <a name="next-steps"></a>Passaggi successivi

[Modifiche del comportamento di SQL Server Reporting Services in SQL Server 2016](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Novità di Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[Funzionalità deprecate di SQL Server Reporting Services in SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[Funzionalità non più disponibili di SQL Server Reporting Services in SQL Server 2016](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
