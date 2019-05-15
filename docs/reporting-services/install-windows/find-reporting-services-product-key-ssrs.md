---
title: Trovare il codice Product Key per SQL Server 2017 Reporting Services | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 36460943b233f02e4d029b7865c7d7fa3844b488
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65502916"
---
# <a name="how-to-find-the-product-key-for-sql-server-2017-reporting-services"></a>Come trovare il codice Product Key per SQL Server 2017 Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Informazioni su come trovare il codice Product Key per SQL Server 2017 Reporting Services per installare il server in un ambiente di produzione.

Per trovare il codice Product Key, per prima cosa scaricare ed eseguire il programma di installazione di SQL Server 2017.

1. Scaricare SQL Server 2017 da una di queste origini:

    - Volume Licensing Service Center
    - Sottoscrizione MSDN
    - Vendita al dettaglio (download da Microsoft Store)

1. Eseguire l'installazione di SQL Server 2017 e copiare il codice prepopolato:

    ![Copiare il codice Product Key per SQL Server 2017](media/find-reporting-services-product-key-ssrs/ssrs-ss2017-copy-product-key.png)

1. [Eseguire l'installazione di Reporting Services](install-reporting-services.md) e incollare la chiave:

     ![Incollare il codice Product Key](media/find-reporting-services-product-key-ssrs/ssrs-ssrs2017-paste-product-key.png)

È necessario eseguire questo passaggio solo la prima volta che si installa SSRS 2017. Per gli aggiornamenti dei servizi non è necessario immettere il codice.

## <a name="related-information"></a>Informazioni correlate

- Per informazioni sull'installazione della modalità nativa di SQL Server Reporting Services, vedere [Installare un server di report di Reporting Services in modalità nativa](install-reporting-services-native-mode-report-server.md). 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

- Per informazioni sull'installazione di SQL Server 2016 Reporting Services e versioni precedenti in modalità integrata SharePoint, vedere [Installare il primo server di report in modalità SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

- [Installare SQL Server 2017 Reporting Services](install-reporting-services.md)
- Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
