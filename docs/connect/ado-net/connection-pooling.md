---
title: Pool di connessioni
description: Informazioni sul pool di connessioni, una tecnica di ottimizzazione usata da ADO.NET per ridurre al minimo il costo dell'apertura delle connessioni alle origini dati.
ms.date: 11/13/2020
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 41b139d2f22a9cb3137879d96224b02eafc24bab
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761499"
---
# <a name="connection-pooling"></a>Pool di connessioni

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La connessione a un'origine dati può richiedere molto tempo. Per ridurre al minimo il costo dell'apertura delle connessioni, ADO.NET usa una tecnica di ottimizzazione denominata *pool di connessioni*, che consente di ridurre il costo associato ad operazioni ripetute di apertura e chiusura delle connessioni.

## <a name="in-this-section"></a>Contenuto della sezione  

[Pool di connessioni SQL Server (ADO.NET)](sql-server-connection-pooling.md)  
Fornisce una panoramica sul pool di connessioni e ne descrive il funzionamento in SQL Server.

## <a name="see-also"></a>Vedere anche

- [Recupero e modifica di dati in ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
