---
title: Modifiche di rilievo di SQL Server Reporting Services in SQL Server 2016 | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41aad02f9f5b65dd1cf1474abd0c152f3face8c0
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503952"
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
