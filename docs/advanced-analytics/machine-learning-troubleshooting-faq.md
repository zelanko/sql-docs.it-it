---
title: Risoluzione dei problemi e domande frequenti per machine learning - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4a62dd0710a97a33f5a4703f194df2c6bcef2a54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650328"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Risolvere i problemi di apprendimento automatico in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Utilizzare questa pagina come punto di partenza per affrontare i problemi noti.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (R e Python)

## <a name="known-issues"></a>Problemi noti

Gli articoli seguenti descrivono i problemi noti con le versioni correnti e precedenti:

+ [Problemi noti per R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Note sulla versione di SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Note sulla versione di SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Come raccogliere informazioni di sistema

Se si è verificato un errore o necessario comprendere un problema nell'ambiente in uso, è importante raccogliere le informazioni correlate in modo sistematico. L'articolo seguente fornisce un elenco di informazioni che facilita la risoluzione dei problemi di supporto autonomo o una richiesta per il supporto tecnico.

+ [Raccolta dei dati per la risoluzione dei problemi di apprendimento automatico](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guide di installazione e configurazione

Iniziare da qui se non è stato configurato machine learning con SQL Server o se si desidera aggiungere la funzionalità:

+ [Installare SQL Server 2017 Machine Learning Services (In-Database)](install/sql-machine-learning-services-windows-install.md)
+ [Installare SQL Server 2017 Machine Learning Server (Standalone)](install/sql-machine-learning-standalone-windows-install.md)
+ [Installare SQL Server 2016 R Services (In-Database)](install/sql-r-services-windows-install.md)
+ [Installare SQL Server 2016 R Server (Standalone)](install/sql-r-standalone-windows-install.md)
+ [Programma di installazione di prompt dei comandi](install/sql-ml-component-commandline-install.md)
+ [Installazione offline (senza Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configurazione

Gli articoli seguenti contengono informazioni sui valori predefiniti e su come personalizzare la configurazione per machine learning in un'istanza di:

+ [Esecuzione simultanea di scalabilità di script esterni in SQL Server Machine Learning Services](administration/modify-user-account-pool.md)   
+ [Configurare e gestire le estensioni di analitica avanzata](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Come creare un pool di risorse](r/how-to-create-a-resource-pool-for-r.md)
+ [Ottimizzazione per carichi di lavoro R](r/operationalizing-your-r-code.md)
