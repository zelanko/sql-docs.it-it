---
description: MSSQLSERVER_41332
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bd040b91e1416dedb6a68317835fe6fcad5b264
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428673"
---
# <a name="mssqlserver_41332"></a>MSSQLSERVER_41332
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41332|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Testo del messaggio|Non è possibile creare o accedere alle tabelle con ottimizzazione per la memoria e alle stored procedure compilate in modo nativo quando la sessione TRANSACTION ISOLATION LEVEL è impostata su SNAPSHOT.|  
  
## <a name="explanation"></a>Spiegazione  
La transazione è stata avviata nel livello di isolamento dello snapshot e quindi ha tentato di utilizzare una funzionalità non compatibile.  
  
## <a name="user-action"></a>Azione dell'utente  
Avviare la transazione con un livello di isolamento diverso. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
[OLTP in memoria &#40;ottimizzazione per la memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
