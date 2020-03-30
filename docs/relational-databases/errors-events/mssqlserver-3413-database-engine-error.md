---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 84f983c9b450e625fdca08c46720a1cf22e8b84c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68098306"
---
# <a name="mssqlserver_3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3413|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|MARKDB|  
|Testo del messaggio|ID di database %d. Impossibile contrassegnare il database come sospetto. Analisi Getnext per NC su sys.databases.database_id non riuscita. Per identificare la causa e correggere gli eventuali problemi associati, fare riferimento agli errori precedenti nel log degli errori.|  
  
## <a name="explanation"></a>Spiegazione  
Si è verificato un errore imprevisto durante il tentativo di contrassegnare un database utente come SUSPECT nel catalogo. Lo stato SUSPECT non sarà persistente.  
  
## <a name="user-action"></a>Azione dell'utente  
Vedere gli errori precedenti e risolvere il problema.  
  
