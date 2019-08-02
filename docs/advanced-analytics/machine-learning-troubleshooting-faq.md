---
title: Risoluzione dei problemi e domande frequenti per Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1573c260c3d34ba3f733316fbae2672b2f9adfb1
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715152"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Risolvere i problemi di Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usare questa pagina come punto di partenza per risolvere i problemi noti.

## <a name="known-issues"></a>Problemi noti

Negli articoli seguenti vengono descritti i problemi noti relativi alle versioni correnti e precedenti:

+ [Problemi noti per R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Note sulla versione di SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Note sulla versione di SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Come raccogliere informazioni di sistema

Se si è verificato un errore o è necessario comprendere un problema nell'ambiente, è importante raccogliere sistematicamente le informazioni correlate. L'articolo seguente fornisce un elenco di informazioni che facilitano la risoluzione dei problemi di supporto autonomo o una richiesta di supporto tecnico.

+ [Raccolta di dati per la risoluzione dei problemi di Machine Learning](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guide all'installazione e alla configurazione

Iniziare da qui se Machine Learning non è stato configurato con SQL Server o se si vuole aggiungere la funzionalità:

+ [Installare SQL Server Machine Learning Services (in-database)](install/sql-machine-learning-services-windows-install.md)
+ [Installa SQL Server Machine Learning Server (standalone)](install/sql-machine-learning-standalone-windows-install.md)
+ [Installazione dal prompt dei comandi](install/sql-ml-component-commandline-install.md)
+ [Installazione offline (senza Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configurazione

Gli articoli seguenti contengono informazioni sui valori predefiniti e su come personalizzare la configurazione per Machine Learning in un'istanza:

+ [Ridimensionare l'esecuzione simultanea di script esterni in SQL Server Machine Learning Services](administration/modify-user-account-pool.md)   
+ [Configurare e gestire Advanced Analytics Extensions](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Come creare un pool di risorse](r/how-to-create-a-resource-pool-for-r.md)
+ [Ottimizzazione per carichi di lavoro R](r/operationalizing-your-r-code.md)
