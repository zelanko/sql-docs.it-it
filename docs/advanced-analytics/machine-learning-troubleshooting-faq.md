---
title: risoluzione dei problemi
description: Rappresenta un punto di partenza per la risoluzione di problemi noti.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c9be3a8dff314f6645029fb54803ad30dc04db27
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727571"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Risolvere i problemi di Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usare questo articolo come punto di partenza per la risoluzione di problemi noti.

## <a name="known-issues"></a>Problemi noti

Gli articoli seguenti descrivono problemi noti relativi alla versione corrente e alle versioni precedenti:

+ [Problemi noti di R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Note sulla versione di SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Note sulla versione di SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Come raccogliere informazioni di sistema

Se si è verificato un errore o è necessario comprendere un problema dell'ambiente, è importante raccogliere sistematicamente informazioni correlate. L'articolo seguente offre un elenco di informazioni che rende più facile risolvere i problemi in modo autonomo o inviare una richiesta di supporto tecnico.

+ [Raccolta di dati per la risoluzione dei problemi di Machine Learning](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guide per l'installazione e la configurazione

Iniziare da qui se non si è ancora eseguita la configurazione di Machine Learning con SQL Server o se si vuole aggiungere la funzionalità:

+ [Installare SQL Server Machine Learning Services (In-Database)](install/sql-machine-learning-services-windows-install.md)
+ [Installare Machine Learning Server per SQL Server (Standalone)](install/sql-machine-learning-standalone-windows-install.md)
+ [Configurazione al prompt dei comandi](install/sql-ml-component-commandline-install.md)
+ [Installazione offline (senza Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configurazione

Gli articoli seguenti contengono informazioni sulle impostazioni predefinite e su come personalizzare la configurazione di Machine Learning in un'istanza:

+ [Ridimensionare l'esecuzione simultanea di script esterni in Machine Learning Services per SQL Server](administration/modify-user-account-pool.md)   
+ [Configurare e gestire Advanced Analytics Extensions](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Come creare un pool di risorse](r/how-to-create-a-resource-pool-for-r.md)
+ [Ottimizzazione per carichi di lavoro R](r/operationalizing-your-r-code.md)
