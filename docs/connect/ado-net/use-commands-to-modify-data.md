---
title: Utilizzo di comandi per modificare i dati
description: Viene descritto come usare un provider di dati per eseguire stored procedure o istruzioni DDL (Data Definition Language).
ms.date: 11/25/2020
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 03ebdbdd15adfae8e765964e8338f043999319f3
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428235"
---
# <a name="using-commands-to-modify-data"></a>Utilizzo di comandi per modificare i dati

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Con il provider di dati Microsoft SqlClient per SQL Server, è possibile eseguire stored procedure o istruzioni Data Definition Language (ad esempio CREATE TABLE e ALTER COLUMN) per eseguire la manipolazione dello schema in un database o in un catalogo. Poiché, diversamente dalle query, questi comandi non restituiscono righe, l'oggetto <xref:Microsoft.Data.SqlClient.SqlCommand> fornisce un metodo <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> per l'elaborazione.

Oltre a usare **ExecuteNonQuery** per modificare lo schema, è possibile usare questo metodo per elaborare istruzioni SQL che modificano i dati ma non restituiscono righe, ad esempio INSERT, UPDATE e DELETE.

Anche se il metodo **ExecuteNonQuery** non restituisce righe, è possibile passare e restituire parametri di input e di output e valori restituiti mediante la raccolta **Parameters** dell'oggetto **Command**.

## <a name="in-this-section"></a>Contenuto della sezione

[Aggiornamento dei dati in un'origine dati](update-data-inside-data-source.md) Viene descritto come eseguire comandi o stored procedure che modificano i dati in un database.

[Esecuzione di operazioni di catalogo](perform-catalog-operations.md) Viene descritto come eseguire i comandi che modificano lo schema del database.

## <a name="see-also"></a>Vedere anche

- [Recupero e modifica di dati in ADO.NET](retrieving-modifying-data.md)
- [Comandi e parametri](commands-parameters.md)
