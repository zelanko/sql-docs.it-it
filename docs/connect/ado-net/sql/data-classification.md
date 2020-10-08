---
title: Individuazione dati e classificazione in SqlClient
description: Viene descritto come controllare se un database di SQL Server supporta la classificazione dei dati e come accedere alle informazioni di classificazione dei dati tramite un oggetto SqlDataReader.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b53e71c4c302145af14c1f2e37f30fe0e3c8f8e2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725722"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Individuazione dati e classificazione in SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[Individuazione dati e classificazione](../../../relational-databases/security/sql-data-discovery-and-classification.md?view=sql-server-2017) è un set di servizi avanzati per l'individuazione, la classificazione, l'assegnazione di etichette e la creazione di report per i dati sensibili nei database. SqlClient fornisce un'API che espone le informazioni di classificazione e individuazione dei dati di sola lettura quando l'origine sottostante supporta la funzionalità. È possibile accedere a queste informazioni tramite SqlDataReader.

Questa applicazione di esempio mostra come accedere alle proprietà di classificazione dei dati di SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Vedere anche**  

 [Funzionalità di SQL Server e ADO.NET](sql-server-features-adonet.md)