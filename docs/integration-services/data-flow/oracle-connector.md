---
title: Connettore Microsoft per Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0ad547d26c86c43b0009cdf20acae33ed7e8ab7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553239"
---
# <a name="microsoft-connector-for-oracle"></a>Connettore Microsoft per Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Connettore Microsoft per Oracle consente di esportare e caricare i dati in un'origine dati Oracle in un pacchetto SSIS.

## <a name="version-support"></a>Supporto versione

I prodotti Microsoft SQL Server seguenti sono supportati da Connettore Microsoft per Oracle:

- A partire da SQL Server 2019
- SQL Server Data Tools (SSDT)

Sono supportate le origini dati delle versioni seguenti di Oracle Database:

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c (senza supporto per l'autenticazione di Windows)

Oracle Database è supportato in tutti i sistemi operativi e le piattaforme.
> [!NOTE]
>
> Il client Oracle non è necessario per Connettore Microsoft per Oracle Database in SQL Server 2019.

## <a name="installation"></a>Installazione

Se è necessario eseguire il pacchetto in SQL Server, è possibile ottenere il programma di installazione di Connettore Microsoft per Oracle Database da [qui](https://www.microsoft.com/en-us/download/details.aspx?id=58228). Quindi, seguire le indicazioni nell'installazione guidata.

Dopo aver installato il connettore, è necessario riavviare il servizio SQL Server Integration Services per assicurarsi che l'origine e la destinazione Oracle funzionino correttamente.

Se è necessario progettare il pacchetto con il connettore, non è necessario scaricare il connettore. È incluso in SQL Server Data Tools (SSDT) a partire dalla versione 15.9.0.

## <a name="uninstallation"></a>Disinstallazione

È possibile eseguire la disinstallazione guidata per rimuovere Connettore Microsoft per Oracle Database da SQL Server.

## <a name="design-ssis-package-with-previous-version"></a>Progettare un pacchetto SSIS con la versione precedente

A partire dalla versione 15.9.0, SSDT include già Connettore Microsoft per Oracle Database, pertanto non è necessaria alcuna installazione per la progettazione di pacchetti SSIS destinati a SQL Server 2019.

Per progettare un pacchetto SSIS destinato a SQL Server 2017 e versioni precedenti, è necessario installare il connettore per Oracle di Attunity per la versione corrispondente.

**Collegamenti per il download:**

- [SQL Server 2017: Connettore Microsoft versione 5.0 per Oracle di Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=55179)
- [SQL Server 2016: Connettore Microsoft versione 4.0 per Oracle di Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=52950)
- [SQL Server 2014: Connettore Microsoft versione 3.0 per Oracle di Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=44582)
- [SQL Server 2012: Connettore Microsoft versione 2.0 per Oracle di Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=29283)

## <a name="next-steps"></a>Passaggi successivi

- Configurare [Gestione connessione Oracle](oracle-connection-manager.md).
- Configurare l'[origine Oracle](oracle-source.md).
- Configurare la [destinazione Oracle](oracle-destination.md).
- Per eventuali domande, visitare [TechCommunity](https://aka.ms/AA5u35j).
