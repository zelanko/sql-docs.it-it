---
title: MSSQLSERVER_2538 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16a79a049ea1b1beaba79ec94c980c73e9614a00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780309"
---
# <a name="mssqlserver_2538"></a>MSSQLSERVER_2538
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|2538|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|Testo del messaggio|File FILE. Numero di extent = EXTENTS, pagine utilizzate = USED_PAGES e pagine riservate = RESERVED_PAGES.|  
  
## <a name="explanation"></a>Spiegazione  
Queste informazioni fanno parte dell'output generato dal comando DBCC CHECKALLOC e riepilogano per ogni file gli extent allocati, le pagine utilizzate e le pagine riservate del database specificato.  
  
## <a name="user-action"></a>Azione dell'utente  
nessuno  
  
