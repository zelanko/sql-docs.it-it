---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 58a6ff1dda1e0694e17d891502c7dca9ebb31c8a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68060577"
---
# <a name="mssqlserver_10737"></a>MSSQLSERVER_10737
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|MSSQLSERVER|  
|ID evento|10737|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|Testo del messaggio|Quando in un'istruzione ALTER TABLE REBUILD o ALTER INDEX REBUILD si specifica una partizione in una clausola DATA_COMPRESSION, è necessario specificare PARTITION=ALL. La clausola PARTITION=ALL viene utilizzata per ribadire che tutte le partizioni della tabella o dell'indice verranno ricompilate anche se nella clausola DATA_COMPRESSION viene specificato un solo subset.|  
  
## <a name="user-action"></a>Azione dell'utente  
Aggiungere la clausola PARTITION=ALL all'istruzione ALTER TABLE o ALTER INDEX. In alternativa, per ricompilare una partizione specifica, usare REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF}).  
  
