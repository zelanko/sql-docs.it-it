---
title: Connettore Microsoft per Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca25b7425ce74cea820e295a6a99bc3a3c1e2817
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755849"
---
# <a name="microsoft-connector-for-teradata-preview"></a>Connettore Microsoft per Teradata (anteprima)
[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Connettore Microsoft per Teradata consente di esportare e caricare i dati in database Teradata all'interno di un pacchetto SSIS.

Questo nuovo connettore supporta database con tabelle abilitate per 1 MB.

## <a name="version-support"></a>Supporto versione

I prodotti Microsoft SQL Server seguenti sono supportati da Connettore Microsoft per Teradata:

- Microsoft SQL Server 2019
- Microsoft SQL Server Data Tools (SSDT)

Microsoft Connector per Teradata usa l'interfaccia del linguaggio di programmazione dell'applicazione Teradata Parallel Transporter per caricare ed esportare dati in e da database Teradata. Sono supportate le versioni seguenti:

- Teradata Parallel Transporter (Teradata PT) 16.10
- Teradata Parallel Transporter (Teradata PT) 16.20

Sono supportate le origini dati delle versioni seguenti di database Teradata:

- Database Teradata 16.20
- Database Teradata 16.10
- Database Teradata 15.10
- Database Teradata 15.00

Per informazioni dettagliate sulla guida per programmatori dell'interfaccia di programmazione dell'applicazione Teradata Parallel Transporter, vedere la [documentazione di Teradata](https://docs.teradata.com/).

## <a name="installation"></a>Installazione

### <a name="prerequisite"></a>Prerequisito

Nei computer a 32 bit installare i seguenti driver da [Teradata Tools and Utilities - Pacchetto di installazione per Windows](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package):

- Driver ODBC Teradata (32 bit)
- API Teradata PT (32 bit)

Nei computer a 64 bit installare i driver seguenti:

- Driver ODBC Teradata (64 bit)
- API Teradata PT (64 bit)

Per installare il connettore per database Teradata, scaricare ed eseguire il programma di installazione dalla [versione più recente di Connettore Microsoft per Teradata](https://www.microsoft.com/download/details.aspx?id=100599). Quindi, seguire le indicazioni nell'installazione guidata.

Dopo aver installato il connettore, è necessario riavviare il servizio SQL Server Integration Services per assicurarsi che l'origine e la destinazione Teradata funzionino correttamente.

Per eseguire il pacchetto SSIS con destinazione SQL Server 2017 e versioni precedenti, è necessario installare il **connettore Microsoft per Teradata di Attunity** con la versione corrispondente dal collegamento seguente:

- [SQL Server 2017: Connettore Microsoft versione 5.0 per Teradata di Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016: Connettore Microsoft versione 4.0 per Teradata di Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014: Connettore Microsoft versione 3.0 per Teradata di Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012: Connettore Microsoft versione 2.0 per Teradata di Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>Disinstallazione

È possibile eseguire la disinstallazione guidata per rimuovere **Connettore Microsoft per Teradata**.

## <a name="next-steps"></a>Passaggi successivi

- Configurare la [gestione connessione Teradata](teradata-connection-manager.md)
- Configurare l'[origine di Teradata](teradata-source.md)
- Configurare la [destinazione di Teradata](teradata-destination.md)
- Per eventuali domande, visitare [TechCommunity](https://aka.ms/AA6iwdw).
