---
description: MSSQLSERVER_3417
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8a7cedd7aec428c7b72d07090356977f385e300
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456204"
---
# <a name="mssqlserver_3417"></a>MSSQLSERVER_3417
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|3417|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|REC_BADMASTER|  
|Testo del messaggio|Impossibile recuperare il database master. Impossibile eseguire SQL Server. Ripristinare il master da un backup completo, correggerlo o ricompilarlo. Per ulteriori informazioni sulla ricompilazione del database master, vedere la documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
Non è possibile avviare il database **master** in SQL Server. Se non è possibile portare online il database **master** o **tempdb**, non è possibile eseguire SQL Server. Questo errore in genere è preceduto da altri errori. Esaminare i log degli errori per individuare la causa radice.  
  
## <a name="user-action"></a>Azione dell'utente  
Ripristinare il backup del database oppure correggere il database.  
  
