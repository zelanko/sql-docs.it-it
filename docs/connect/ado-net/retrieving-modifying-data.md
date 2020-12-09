---
title: Recupero e modifica di dati
description: In .NET Framework, il provider di dati Microsoft SqlClient per SQL Server funge da ponte tra un'applicazione e un'origine dati per la lettura e l'aggiornamento dei dati.
ms.date: 11/13/2020
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 8fc6a8ed3cf4fec9b97b81c38fb1667588623ba7
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419741"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>Recupero e modifica di dati in ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La connessione a un'origine dati e il recupero dei dati in essa contenuti sono funzioni fondamentali nelle applicazioni di database. Il provider di dati SqlClient funge da ponte tra un'applicazione e un'origine dati, consentendo di eseguire comandi e di recuperare dati tramite un **DataReader** o un **DataAdapter**. Una funzione chiave di qualsiasi applicazione di database è la capacità di aggiornare i dati archiviati nel database. Nel provider di dati Microsoft SqlClient per SQL Server l'aggiornamento dei dati prevede l'uso di oggetti **DataAdapter**, <xref:System.Data.DataSet> e **Command**. Può anche prevedere l'uso di transazioni.

## <a name="in-this-section"></a>Contenuto della sezione

[Connessione a un'origine dati](connecting-to-data-source.md) Descrive come stabilire una connessione a un'origine dati e come usare gli eventi di connessione.

[Stringhe di connessione](connection-strings.md) Contiene argomenti che descrivono diversi aspetti dell'uso delle stringhe di connessione, tra cui le parole chiave, le informazioni di sicurezza e l'archiviazione e il recupero delle stringhe di connessione stesse.

[Pool di connessioni](connection-pooling.md) Descrive i pool di connessioni per il provider di dati Microsoft SqlClient per SQL Server.

## <a name="see-also"></a>Vedere anche

- [Mapping dei tipi di dati in ADO.NET](data-type-mappings-ado-net.md)
- [SQL Server e ADO.NET](./sql/index.md)
