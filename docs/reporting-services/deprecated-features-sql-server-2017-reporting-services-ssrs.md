---
title: Funzionalità deprecate di SQL Server 2017 Reporting Services | Microsoft Docs
description: Questo articolo descrive le funzionalità che saranno deprecate nella prossima versione di SQL Server Reporting Services.
ms.date: 11/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fe51ce9d86688669e84ad866ad9f5e6da075e8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74320315"
---
# <a name="deprecated-features-in-sql-server-2017-reporting-services"></a>Funzionalità deprecate in SQL Server 2017 Reporting Services

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017](../includes/ssrs-appliesto-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

Il fatto di indicare una funzionalità come deprecata significa quanto segue:

- La funzionalità è solo in modalità manutenzione. Non verranno apportate nuove modifiche, incluse quelle per l'interoperabilità con le nuove funzionalità.
- Microsoft si impegna a non rimuovere una funzionalità deprecata dalle versioni future per semplificare gli aggiornamenti. Tuttavia, in rari casi, una funzionalità potrebbe essere rimossa in modo permanente da Reporting Services se limita le innovazioni future.
- Per i nuovi progetti di sviluppo, non è consigliabile usare funzionalità deprecate.

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>Funzionalità deprecate nella prossima versione di SQL Server

Le funzionalità seguenti di SQL Server Reporting Services 2017 non saranno supportate nella prossima versione di SQL Server. Non implementare queste funzionalità in nuovi progetti di sviluppo e, appena possibile, modificare le applicazioni in cui sono attualmente usate.

> [!NOTE]
> Questo elenco è identico all'elenco di SQL Server 2016 Reporting Services (13.x). Non sono annunciate funzionalità nuove o deprecate per SQL Server 2017 Reporting Services (14.x).


| **Categoria** | **Funzionalità deprecata** | **Sostituzione** |
| --- | --- | --- |
| Server di report | Renderer HTML 4.0. | Renderer HTML 5 |

## <a name="see-also"></a>Vedere anche

[Funzionalità non più supportate in SQL Server Reporting Services (SSRS)](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
