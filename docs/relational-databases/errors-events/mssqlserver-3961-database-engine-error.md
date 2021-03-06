---
description: MSSQLSERVER_3961
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 837215560e15ff01a84f614ac087ff96930db3cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456134"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|3961|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|XACT_METADATA_INVALID|  
|Testo del messaggio|Transazione di isolamento snapshot non riuscita nel database '%. * ls' perché l'oggetto a cui accede l'istruzione è stato modificato da un'istruzione DDL in un'altra transazione simultanea fin dall'inizio di questa transazione.  È stata respinta perché i metadati non sono sottoposti al controllo delle versioni. Un aggiornamento simultaneo ai metadati può causare incoerenze se combinato con l'isolamento dello snapshot.|  
  
## <a name="explanation"></a>Spiegazione  
Questo errore può verificarsi se si esegue una query nei metadati nell'isolamento dello snapshot ed è presente un'istruzione DDL simultanea che aggiorna i metadati a cui si accede nell'isolamento dello snapshot. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta il controllo delle versioni dei metadati. Per questo motivo, esistono restrizioni sulle operazioni DDL che è possibile eseguire all'interno di una transazione esplicita in esecuzione nell'isolamento dello snapshot. Per definizione, una transazione implicita è una singola istruzione che rende possibile applicare la semantica dell'isolamento dello snapshot anche con istruzioni DDL. Le istruzioni DDL seguenti non sono consentite con l'isolamento snapshot dopo un'istruzione BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME o qualsiasi istruzione DDL di Common Language Runtime (CLR). Queste istruzioni sono consentite quando si usa l'isolamento dello snapshot all'interno di transazioni implicite. Per definizione, una transazione implicita è una singola istruzione che rende possibile applicare la semantica dell'isolamento dello snapshot anche con istruzioni DDL.  
  
## <a name="user-action"></a>Azione dell'utente  
Spostare il livello di isolamento dello snapshot su un livello di isolamento non snapshot ad esempio Read committed prima di eseguire una query sui metadati.  
  
