---
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
ms.openlocfilehash: a9456aed02e9e1a2566bf0281dacd07f435af44b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728370"
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
  
