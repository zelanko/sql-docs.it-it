---
title: Funzionalità deprecate di SQL Server 2019 Reporting Services | Microsoft Docs
description: Questo articolo descrive le funzionalità che saranno deprecate nella prossima versione di SQL Server Reporting Services.
ms.date: 11/21/2019
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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: eaa7edebe99a7c444fe1bfa23971317517399ea2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74320275"
---
# <a name="deprecated-features-in-sql-server-2019-reporting-services"></a>Funzionalità deprecate in SQL Server 2019 Reporting Services

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2019-and-later](../includes/ssrs-appliesto-2019-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../includes/ssrs-appliesto-pbirs.md)]

Il fatto di indicare una funzionalità come deprecata significa quanto segue:

- La funzionalità è solo in modalità manutenzione. Non verranno apportate nuove modifiche, incluse quelle per l'interoperabilità con le nuove funzionalità.
- Microsoft si impegna a non rimuovere una funzionalità deprecata dalle versioni future per semplificare gli aggiornamenti. Tuttavia, in rari casi, una funzionalità potrebbe essere rimossa in modo permanente da Reporting Services se limita le innovazioni future.
- Per i nuovi progetti di sviluppo, non è consigliabile usare funzionalità deprecate.

**Funzionalità deprecate in una versione futura di SQL Server**

SQL Server Reporting Services supporta le seguenti funzionalità nella versione successiva di SQL Server, ma queste funzionalità risulteranno deprecate in una versione successiva. La versione specifica di SQL Server non è stata determinata.

| **Categoria** | **Funzionalità deprecata** | **Sostituzione** |
| --- | --- | --- |
| Server di report | Raccolta parti del report | nessuno |
| Server di report | Report per dispositivi mobili e Mobile Report Publisher | I report di Power BI nel server di report di Power BI offrono funzionalità per dispositivi mobili. |
| Server di report | Formati di rendering XLS e DOC | I formati XLSX e DOCX sono disponibili e supportati. |
| Server di report | Feed di dati Atom | Il supporto del feed oData è disponibile per i set di dati condivisi in SSRS e nel server di report di Power BI. |

## <a name="see-also"></a>Vedere anche

[Funzionalità non più supportate in SQL Server 2019 Reporting Services (SSRS)](discontinued-functionality-sql-server-reporting-services-2019.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
