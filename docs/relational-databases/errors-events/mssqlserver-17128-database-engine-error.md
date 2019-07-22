---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 210df5d533908e75e83b348ac6c9a84a22198f4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131820"
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17128|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|INIT_NOBUFSPACE|  
|Testo del messaggio|initdata: memoria non disponibile per i buffer del kernel.|  
  
## <a name="explanation"></a>Spiegazione  
Non è stato possibile eseguire le allocazioni o le prenotazioni iniziali di memoria per il pool di buffer. SQL Server viene chiuso.  
  
## <a name="user-action"></a>Azione dell'utente  
Questo errore si verifica in genere quando SQL Server viene avviato in un computer con requisiti di sistema estremamente inferiori rispetto a quelli minimi necessari.  
  
