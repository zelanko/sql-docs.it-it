---
description: MSSQLSERVER_9790
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 04ead56d08fb1e2214a99c9ec4dcefb4d816660e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460834"
---
# <a name="mssqlserver_9790"></a>MSSQLSERVER_9790
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|9790|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Testo del messaggio|Impossibile eseguire il routing del messaggio in arrivo. Il database di sistema MSDB contenente le informazioni di routing è in modalità utente singolo.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un errore durante il tentativo di classificare un messaggio ricevuto fuori collegamento poiché il database MSDB è in modalità utente singolo.  
  
## <a name="user-action"></a>Azione dell'utente  
Impostare MSDB sulla modalità MULTI USER con il comando ALTER DATABASE.  
  
