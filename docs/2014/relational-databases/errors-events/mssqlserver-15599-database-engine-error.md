---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e377f8257000fc2e0695c2ef2624622760f1facb
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553756"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|15599|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Testo del messaggio|Impossibile impostare controllo e autorizzazioni in oggetti temporanei locali.|  
  
## <a name="explanation"></a>Spiegazione  
 Il controllo e le autorizzazioni non hanno alcuno effetto quando si impostano oggetti temporanei locali o globali. Le istruzioni non restituiscono un errore e verranno eseguite correttamente, ma non hanno effetto.  
  
 Questo comportamento non viene modificato. Tuttavia, a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], il messaggio ha lo scopo informativo di avvisare l'utente.  
  
## <a name="user-action"></a>Azione dell'utente  
 Non è necessaria alcuna azione, ma è opportuno prendere in considerazione la rimozione delle istruzioni che tentano di impostare controllo o autorizzazioni sugli oggetti temporanei locali o globali.  
  
  
