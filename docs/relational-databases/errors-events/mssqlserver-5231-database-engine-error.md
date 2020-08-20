---
description: MSSQLSERVER_5231
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 634b525a3daa2b5ac83a759c89c8edd52eb5ca6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471037"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|5231|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|Testo del messaggio|ID oggetto O_ID (oggetto 'NAME'): si è verificato un deadlock durante il tentativo di bloccare questo oggetto per la verifica. L'oggetto è stato ignorato e non verrà elaborato.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un deadlock durante il tentativo da parte di DBCC di bloccare l'oggetto e DBCC è stato scelto come vittima del deadlock. L'oggetto non verrà elaborato.  
  
## <a name="user-action"></a>Azione dell'utente  
nessuno  
  
