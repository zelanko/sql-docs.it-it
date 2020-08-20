---
description: MSSQLSERVER_5554
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f8039ad4a6cfefcdbd4e72c583f520e36f273875
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470909"
---
# <a name="mssqlserver_5554"></a>MSSQLSERVER_5554
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|MSSQLSERVER|  
|ID evento|5554|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|FS_MINIVER_OVERFLOW|  
|Testo del messaggio|È stato raggiunto il limite massimo di versioni totali per un singolo supportato dal file system.|  
  
## <a name="explanation"></a>Spiegazione  
In scenari MARS (Multiple Active Result Set) o con presenza di trigger, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la miniversione specificata dal sistema operativo.  
  
## <a name="user-action"></a>Azione dell'utente  
Tentare di evitare aggiornamenti ripetuti ai dati nella stessa transazione.  
  
