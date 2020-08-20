---
description: MSSQLSERVER_3937
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 90e05045031d4bab8c2975a6e2349df85ca588c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456151"
---
# <a name="mssqlserver_3937"></a>MSSQLSERVER_3937
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|MSSQLSERVER|  
|ID evento|3937|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Testo del messaggio|Durante il rollback di una transazione, si è verificato un errore nel tentativo di notificare l'esecuzione del rollback di una transazione al driver del filtro FILESTREAM. Codice errore: 0x%0x.|  
  
## <a name="explanation"></a>Spiegazione  
Durante l'invio di una notifica di esecuzione del rollback di una transazione, è stato restituito un errore dal driver RsFx, probabilmente a causa di risorse insufficienti. Questa situazione potrebbe provocare una piccola perdita di memoria nel driver del filtro RsFx, in cui tuttavia verrà liberato spazio quando il processo sqlservr.exe che creato la transazione termina.  
  
## <a name="user-action"></a>Azione dell'utente  
