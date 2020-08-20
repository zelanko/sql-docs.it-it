---
description: MSSQLSERVER_5515
title: MSSQLSERVER_5515 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: aecbc4ad6ee5c3f8a0ebcf596dca0a06392acedf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470908"
---
# <a name="mssqlserver_5515"></a>MSSQLSERVER_5515
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|MSSQLSERVER|  
|ID evento|5515|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|FS_OPEN_CONTAINER_FAILED|  
|Testo del messaggio|Impossibile aprire la directory contenitore ''%.*ls'' del file FILESTREAM. Il sistema operativo ha restituito il codice di stato di Windows 0x%x.|  
  
## <a name="explanation"></a>Spiegazione  
La directory contenitore del file FILESTREAM specificata non può essere aperta.  
  
## <a name="user-action"></a>Azione dell'utente  
Per la causa dell'errore, vedere il codice di stato di Windows specifico.  
  
