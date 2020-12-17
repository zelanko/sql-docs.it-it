---
title: Risolvere i problemi di Machine Learning in SQL Server
description: Viene fornito un punto di partenza per risolvere i problemi di Machine Learning in SQL.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/31/2018
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: e2d4d278f48cd453afb0666d0c9752c86b4a7e65
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470622"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Risolvere i problemi di Machine Learning in SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Usare questo articolo come punto di partenza per la risoluzione dei problemi che si verificano quando si usa Machine Learning in SQL Server.

## <a name="known-issues"></a>Problemi noti

Gli articoli seguenti descrivono problemi noti relativi alla versione corrente e alle versioni precedenti:

+ [Problemi noti di R Services](known-issues-for-sql-server-machine-learning-services.md)
+ [Note sulla versione di SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md)
+ [Note sulla versione di SQL Server 2017](../../sql-server/sql-server-2017-release-notes.md)
+ [Note sulla versione di SQL Server 2019](../../sql-server/sql-server-version-15-release-notes.md)

## <a name="how-to-gather-system-information"></a>Come raccogliere informazioni di sistema

Se si è verificato un errore o è necessario comprendere un problema dell'ambiente, è importante raccogliere sistematicamente informazioni correlate. L'articolo seguente offre un elenco di informazioni che rende più facile risolvere i problemi in modo autonomo o inviare una richiesta di supporto tecnico.

+ [Raccolta di dati per la risoluzione dei problemi di Machine Learning](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guide per l'installazione e la configurazione

Iniziare da qui se non si è ancora eseguita la configurazione di Machine Learning con SQL Server o se si vuole aggiungere la funzionalità:

+ [Installare SQL Server Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Installare Machine Learning Server per SQL Server (Standalone)](../install/sql-machine-learning-standalone-windows-install.md)
+ [Configurazione al prompt dei comandi](../install/sql-ml-component-commandline-install.md)
+ [Installazione offline (senza Internet)](../install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configurazione

Gli articoli seguenti contengono informazioni sulle impostazioni predefinite e su come personalizzare la configurazione di Machine Learning in un'istanza di SQL:

+ [Ridimensionare l'esecuzione simultanea di script esterni in Machine Learning Services per SQL Server](../administration/scale-concurrent-execution-external-scripts.md)   
+ [Come creare un pool di risorse](../administration/create-external-resource-pool.md)
+ [Ottimizzazione per carichi di lavoro R](../r/operationalizing-your-r-code.md)
