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
ms.openlocfilehash: 98127e41b5b07c38030ef27214c9c92bf7c4b4be
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761479"
---
# <a name="using-commands-to-modify-data"></a>Utilizzo di comandi per modificare i dati

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Con il provider di dati Microsoft SqlClient per SQL Server, è possibile eseguire stored procedure o istruzioni Data Definition Language (ad esempio CREATE TABLE e ALTER COLUMN) per eseguire la manipolazione dello schema in un database o in un catalogo. Poiché, diversamente dalle query, questi comandi non restituiscono righe, l'oggetto <xref:Microsoft.Data.SqlClient.SqlCommand> fornisce un metodo <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> per l'elaborazione.

Oltre a usare **ExecuteNonQuery** per modificare lo schema, è possibile usare questo metodo per elaborare istruzioni SQL che modificano i dati ma non restituiscono righe, ad esempio INSERT, UPDATE e DELETE.

Anche se il metodo **ExecuteNonQuery** non restituisce righe, è possibile passare e restituire parametri di input e di output e valori restituiti mediante la raccolta **Parameters** dell'oggetto **Command**.

## <a name="in-this-section"></a>Contenuto della sezione

[Aggiornamento di dati in un'origine dati](update-data-inside-data-source.md)  
Viene descritto come eseguire i comandi o le stored procedure che modificano i dati in un database.

[Esecuzione di operazioni di catalogo](perform-catalog-operations.md)  
Viene descritto come eseguire i comandi per la modifica dello schema di database.

## <a name="see-also"></a>Vedere anche

- [Recupero e modifica di dati in ADO.NET](retrieving-modifying-data.md)
- [Comandi e parametri](commands-parameters.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
