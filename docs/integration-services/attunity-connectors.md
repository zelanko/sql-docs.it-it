---
title: Connettori Microsoft per Oracle e Teradata di Attunity | Microsoft Docs
ms.date: 08/16/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bcf543438e3d1490f74df7a92a12545f29eeb5f2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "77903831"
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Connettori Microsoft per Oracle e Teradata di Attunity per Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

> [!NOTE]
> I connettori Attunity per Oracle e Teradata supportano SQL Server 2017 e versioni precedenti.
>
> A partire da SQL Server 2019, è possibile ottenere i connettori più recenti per Oracle e Teradata qui:
> - [Connettore Microsoft per Oracle](data-flow/oracle-connector.md)
> - [Connettore Microsoft per Teradata](data-flow/teradata-connector.md)

È possibile scaricare connettori per Integration Services di Attunity che ottimizzano le prestazioni quando si caricano i dati in o da Oracle o Teradata in un pacchetto SSIS.

## <a name="download-the-latest-attunity-connectors"></a>Scaricare i connettori di Attunity più recenti

Ottenere qui la versione più recente dei connettori:  
[Connettori Microsoft v5.0 per Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problema: i connettori di Attunity non sono visibili nella casella degli strumenti SSIS

Per visualizzare i connettori di Attunity nella casella degli strumenti SSIS, è sempre necessario installare la versione dei connettori che ha come destinazione la versione di SQL Server corrispondente a quella di SQL Server Data Tools (SSDT) installato nel computer in uso. (L'utente potrebbe avere versioni precedenti dei connettori installati.) Questo requisito è indipendente dalla versione di SQL Server che si vuole avere come destinazione per i progetti e pacchetti SSIS.

Se ad esempio è installata la versione più recente di SSDT, si ha la versione 17 di SSDT con un numero di build che inizia con 14. Questa versione di SSDT aggiunge il supporto per SQL Server 2017. Per visualizzare e usare i connettori di Attunity nello sviluppo del pacchetto SSIS, anche se si vuole avere come destinazione una versione precedente di SQL Server, è necessario installare anche la versione più recente dei connettori di Attunity, la versione 5.0. Questa versione dei connettori aggiunge anche il supporto per SQL Server 2017.

Controllare la versione installata di SSDT in Visual Studio da **Guida** | **Informazioni su Microsoft Visual Studio** o in **Programmi e funzionalità** nel Pannello di controllo. Installare quindi la versione corrispondente dei connettori di Attunity dalla tabella seguente.

|Versione SSDT|Numero di build SSDT|Versione di SQL Server di destinazione|Versione richiesta dei connettori|
|---------|---------|---------|---------|
|17|Inizia con 14|SQL Server 2017|[Connettori Microsoft v5.0 per Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Inizia con 13|SQL Server 2016|[Connettori Microsoft v4.0 per Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Scaricare la versione più recente di SQL Server Data Tools (SSDT)

Ottenere la versione più recente di SSDT qui:  
[Scaricare la versione più recente di SQL Server Data Tools](..//ssdt/download-sql-server-data-tools-ssdt.md)
