---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 86d99f8223cf969e5e28a6ae3eb6d453e3c07857
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68043577"
---
# <a name="mssqlserver_3619"></a>MSSQLSERVER_3619
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3619|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SYS_NOLOG|  
|Testo del messaggio|Impossibile scrivere un record di checkpoint nel database con ID %d perché nel log non è disponibile spazio. Rivolgersi all'amministratore di sistema per troncare il log o per allocare più spazio per i file dei log del database.|  
  
## <a name="explanation"></a>Spiegazione  
Lo spazio nel log delle transazioni è esaurito.  
  
## <a name="user-action"></a>Azione dell'utente  
Troncare il log per liberare spazio oppure allocare ulteriore spazio per il log. Per ulteriori informazioni, vedere "Risoluzione dei problemi relativi a un log delle transazioni pieno (Errore 9002)" nella documentazione online di SQL Server.  
  
