---
title: SQL Server con abilitazione di Azure Arc - Note sulla versione
description: Note sulla versione più recenti
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 10/29/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3dcbc6b17d5abe87aabe923d70746d65595b9de6
ms.sourcegitcommit: dc3ea1696b8a4332934568439aed6cce4e9737eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244653"
---
# <a name="release-notes---azure-arc-enabled-sql-server-preview"></a>Note sulla versione - SQL Server con abilitazione di Azure Arc (anteprima)

> [!NOTE]
> In quanto funzionalità di anteprima, la tecnologia presentata in questo articolo è soggetta alle [condizioni per l'utilizzo supplementari per le anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="september-2020"></a>Settembre 2020

SQL Server con abilitazione di Azure Arc è stato rilasciato per l'anteprima pubblica. SQL Server con abilitazione di Azure Arc estende i servizi di Azure alle istanze di SQL Server ospitate all'esterno di Azure nel data center del cliente, nella rete perimetrale o in un ambiente multi-cloud.

Per informazioni dettagliate, vedere [Panoramica di SQL Server con abilitazione di Azure Arc](overview.md)

### <a name="known-issues"></a>Problemi noti

Nella versione di settembre sono presenti i problemi seguenti:

* Il pannello **Register Azure Arc Enabled SQL Server** (Registra SQL Server con abilitazione di Azure Arc) non supporta la configurazione di tag personalizzati. Per aggiungere tag personalizzati, aprire la risorsa **SQL Server - Azure Arc** dopo la registrazione e modificare i tag nella pagina **Panoramica**.

* Per la connessione di istanze di SQL Server ad Azure Arc è necessario un account con un ampio set di autorizzazioni. Per informazioni dettagliate, vedere [Autorizzazioni necessarie](overview.md#required-permissions).

## <a name="october-2020"></a>Ottobre 2020

L'aggiornamento di ottobre include i miglioramenti seguenti:

* Il pannello Register Azure Arc Enabled SQL Server (Registra SQL Server con abilitazione di Azure Arc) include ora la scheda **Tag**. I tag sono inclusi nello script di registrazione e si riflettono nelle risorse **SQL Server - Azure Arc**. Per informazioni dettagliate, vedere [Connettere l'istanza di SQL Server ad Azure Arc](connect.md).

* La voce **Environment Health** (Integrità ambiente) supporta ora l'attivazione di **Valutazione SQL** dal portale tramite la distribuzione di una *CustomScriptExtension*. Per informazioni dettagliate, vedere [Configurare Valutazione SQL](assess.md#run-on-demand-sql-assessment).

### <a name="known-issues"></a>Problemi noti

Nella versione di ottobre sono presenti i problemi seguenti:

* Per la connessione di istanze di SQL Server ad Azure Arc è necessario un account con un ampio set di autorizzazioni. Per informazioni dettagliate, vedere [Autorizzazioni necessarie](overview.md#required-permissions).

## <a name="next-steps"></a>Passaggi successivi

**Si desidera fare semplicemente una prova?**  Iniziare rapidamente con la [guida di avvio rapido per SQL Server con abilitazione di Azure Arc](https://aka.ms/AzureArcSqlServerJumpstart).
