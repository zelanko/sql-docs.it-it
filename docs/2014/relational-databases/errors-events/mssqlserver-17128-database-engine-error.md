---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0e08c668acd0a8b2decb14da338b8d1f1e650de5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967890"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
    
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
  
  
