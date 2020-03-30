---
title: MSSQLSERVER_18264 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18264 (Database Engine error)
ms.assetid: 3050fc56-2be5-43cf-916b-50a3ac5f89aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: df0bd7c7093aeb46421fca75c9e9233f2b1f4263
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68137127"
---
# <a name="mssqlserver_18264"></a>MSSQLSERVER_18264
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|Microsoft SQL Server|  
|ID evento|18264|  
|Origine evento|MSSQLENGINE|  
|Componente|SQLEngine|  
|Nome simbolico|STRMIO_DBDUMP|  
|Testo del messaggio|Backup del database eseguito: database: %s, data (ora) di creazione: %s(%s), pagine copiate: %d, primo LSN: %s, ultimo LSN: %s, numero di dispositivi di dump: %d, informazioni dispositivo: (%s). Questo è un messaggio informativo. Non è richiesta alcuna azione da parte dell'utente.|  
  
## <a name="explanation"></a>Spiegazione  
Per impostazione predefinita, per ogni backup eseguito in modo corretto viene aggiunto questo messaggio informativo al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e al registro eventi di sistema. Se il backup del log delle transazioni viene eseguito di frequente, questi messaggi possono aumentare rapidamente, provocando la creazione di log degli errori di grandi dimensioni e rendendo difficile l'individuazione di altri messaggi.  
  
## <a name="user-action"></a>Azione dell'utente  
È possibile eliminare queste voci di log mediante il flag di traccia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]3226**di**. L'abilitazione di questo flag di traccia risulta utile se si eseguono backup del log frequenti e se nessuno degli script dipende da tali voci.  
  
Per informazioni sull'utilizzo dei flag di traccia, vedere la documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
[Flag di traccia &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
