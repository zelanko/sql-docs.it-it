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
ms.openlocfilehash: e3a2d500a16a90ce997273fad3eb7c2d8a82c1d6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553676"
---
# <a name="mssqlserver_17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
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
  
  
