---
title: Log degli errori di SQL Server (gruppi di disponibilità)
description: Informazioni sugli eventi del log degli errori di SQL Server che interessano un gruppo di disponibilità Always On e quali sintomi dovrebbero portare alla revisione del log degli errori.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: b33827f37d02edf783c4688c9ad08cd4673706e7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670885"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>Log degli errori di SQL Server (Gruppi di disponibilità Always On)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Il log degli errori di SQL Server segnala gli eventi che interessano Gruppi di disponibilità Always On, ad esempio:  
  
-   Comunicazione con il cluster WSFC (Windows Server Failover Clustering)    
-   Transizioni di stato delle replica di disponibilità    
-   Transizioni di stato dei database di disponibilità    
-   Stato di connettività dei database di disponibilità tra repliche primarie e secondarie    
-   Stati degli endpoint del gruppo di disponibilità    
-   Stati dei listener del gruppo di disponibilità    
-   Stato di lease tra la DLL risorse SQL Server (in esecuzione nel cluster WSFC) e l'istanza di SQL Server (per altre informazioni, vedere [How It Works: SQL Server Always On Lease Timeout](/archive/blogs/psssql/how-it-works-sql-server-alwayson-lease-timeout) (Funzionamento: timeout lease di SQL Server Always On)    
-   Eventi di errore nel gruppo di disponibilità  

Esaminare il log degli errori di SQL Server rivedendo i sintomi seguenti:  

-   Impossibile accedere ai database di disponibilità    
-   Failover imprevisto del gruppo di disponibilità    
-   Gruppo di disponibilità inaspettatamente con lo stato Risoluzione in corso    
-   Gruppo di disponibilità in uno stato indeterminato  
  
Per altre informazioni, vedere [View the SQL Server error log &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md) (Visualizzare il log degli errori di SQL Server &#40;SQL Server Management Studio&#41)  
  
