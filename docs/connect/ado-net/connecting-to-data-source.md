---
title: Connessione a un'origine dati
description: Informazioni sugli oggetti Connection, usati per connettersi alle origini dati in ADO.NET. L'oggetto Connection usato dipende dal tipo dell'origine dati.
ms.date: 11/13/2020
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 26554deb5d8a3786efd1bd869a2692d368132531
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419812"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>Connessione a un'origine dati in ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Nel provider di dati Microsoft SqlClient è possibile usare un oggetto **Connection** per connettersi a un'origine dati specifica inserendo le informazioni di autenticazione necessarie in una stringa di connessione. L'oggetto **Connection** usato dipende dal tipo dell'origine dati.

Il provider di dati Microsoft SqlClient per SQL Server include un tipo <xref:Microsoft.Data.SqlClient.SqlConnection> derivato da una classe <xref:System.Data.Common.DbConnection>.

## <a name="in-this-section"></a>Contenuto della sezione  

[Stabilire la connessione](establishing-connection.md)\
Viene descritto come usare un oggetto **Connection** per stabilire una connessione a un'origine dati.

[Eventi di connessione](connection-events.md)\
Viene descritta la procedura per usare un evento **InfoMessage** per recuperare i messaggi informativi da un'origine dati.

## <a name="see-also"></a>Vedere anche

- [Stringhe di connessione](connection-strings.md)
- [Pool di connessioni](connection-pooling.md)
