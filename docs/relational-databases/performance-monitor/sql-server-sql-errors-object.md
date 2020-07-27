---
title: Oggetto SQL Errors di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto SQLServer:SQL Errors, che fornisce i contatori per monitorare gli errori di SQL in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 8d2b511f76fd659f1fcb3bd37d4041d57603b3cd
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457973"
---
# <a name="sql-server-sql-errors-object"></a>Oggetto Errori SQL di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'oggetto **SQLServer:Errori SQL** di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include contatori che consentono di monitorare **Errori SQL**.  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto **SQL Errors** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contatori dell'oggetto Errori SQL di SQLServer|Descrizione|  
|------------------------------------|-----------------|  
|**Errori/sec**|Numero di errori/sec|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Elemento|Definizione|  
|----------|----------------|  
|**_Total**|Informazioni relative a tutti gli errori.|  
|**DB Offline Errors**|Tiene traccia degli errori gravi che obbligano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a impostare il database corrente come offline.|  
|**Info Errors**|Informazioni relative a messaggi di errore di tipo informativo che non provocano errori.|  
|**Kill Connection Errors**|Tiene traccia degli errori gravi che obbligano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a terminare la connessione corrente.|  
|**User Errors**|Informazioni sugli errori dell'utente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
