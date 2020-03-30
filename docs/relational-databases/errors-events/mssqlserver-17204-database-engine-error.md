---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 555a7c6f0573836ee4afb95b91ce6e8b84ac6ee5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68131687"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17204|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBLKIO_DEVOPENFAILED|  
|Testo del messaggio|%ls: Impossibile aprire il file %ls per il numero di file %d.  Errore del sistema operativo: %ls.|  
  
## <a name="explanation"></a>Spiegazione  
SQL Server non è stato in grado di aprire il file specificato a causa dell'errore indicato.  
  
## <a name="user-action"></a>Azione dell'utente  
Diagnosticare e correggere l'errore del sistema operativo, quindi ripetere l'operazione.  
  
