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
ms.openlocfilehash: 27b9c232fe785d3c016848f3bb952236b8e7cd75
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110125"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Individuazione dati e classificazione in SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[Individuazione dati e classificazione](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017) è un set di servizi avanzati per l'individuazione, la classificazione, l'assegnazione di etichette e la creazione di report per i dati sensibili nei database. SqlClient fornisce un'API che espone le informazioni di classificazione e individuazione dei dati di sola lettura quando l'origine sottostante supporta la funzionalità. È possibile accedere a queste informazioni tramite SqlDataReader.

Questa applicazione di esempio mostra come accedere alle proprietà di classificazione dei dati di SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Vedere anche**  

 [Funzionalità di SQL Server e ADO.NET](sql-server-features-adonet.md)   
