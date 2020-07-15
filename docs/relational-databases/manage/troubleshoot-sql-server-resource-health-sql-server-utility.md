---
title: Risolvere i problemi relativi all'integrità delle risorse di SQL Server (Utilità SQL Server) | Microsoft Docs
description: Informazioni sulla risoluzione dei problemi di integrità delle risorse identificati da un punto di controllo dell'utilità di SQL Server, ad esempio il sovrautilizzo di CPU, spazio file o spazio su disco allocato.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cb188aa5a71ef9631aa61ead08cfc33ed1210c7f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786444"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>Risoluzione dei problemi relativi all'integrità delle risorse di SQL Server (Utilità SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La risoluzione dei problemi di integrità delle risorse identificati da un punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe includere la riduzione di una CPU sovrautilizzata su un computer o su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oppure la riduzione di una CPU sovrautilizzata per un'applicazione del livello dati. Altri problemi potrebbero includere la risoluzione dello spazio file sovrautilizzato per i file di database o la risoluzione del sovrautilizzo dello spazio su disco allocato su un volume di archiviazione.  
  
 Si noti che se il database si trova in stato di "emergenza", lo stato di integrità visualizzerà lo spazio sovrautilizzato del file di log.  
  
 Per altre informazioni sulla raccolta dati con errori che comporta icone di stato grigie nella visualizzazione elenco dell'istanza gestita su un punto di controllo dell'utilità, vedere [Risoluzione dei problemi relativi a Utilità SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453). Per altre informazioni sulle attività iniziali con Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Per ulteriori informazioni sulla riduzione dei problemi di integrità specifici delle risorse identificati da un punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere gli argomenti seguenti.  
  
-   [Identificazione della versione e dell'edizione di SQL Server](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [Risoluzione dei problemi relativi alle prestazioni in SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=151354)  
  
  
