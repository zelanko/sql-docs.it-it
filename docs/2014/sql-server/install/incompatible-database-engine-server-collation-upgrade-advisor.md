---
title: Regole di confronto del Database non compatibile motore Server (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 235811baf7339416750a5e3795caae55b0ba70aa
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094747"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Regole di confronto del server del motore di database incompatibili (Upgrade Advisor)
  Preparazione aggiornamento ha rilevato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizza un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che è configurato per utilizzare una regola di confronto server incompatibili.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 Preparazione aggiornamento ha rilevato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizza un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che è configurato per utilizzare una regola di confronto server incompatibili.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint viene utilizzata l'architettura di servizi condivisi SharePoint. In SharePoint non viene supportato [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurato per la distinzione tra maiuscole e minuscole o per regole di confronto del server o per regole di confronto del server binarie. Le regole di confronto incompatibili includono regole di confronto che per impostazione predefinita supportano la distinzione tra maiuscole e minuscole o che sono binarie e regole di confronto di base che per impostazione predefinita sono compatibili ma sono state configurate con alcune delle designazioni delle regole di confronto seguenti:  
  
-   **Binario**  
  
-   **Distinzione maiuscole/minuscole**  
  
-   **Binary-codepoint**  
  
 Poiché le regole di confronto del server [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] correnti sono incompatibili, l'aggiornamento è bloccato.  
  
## <a name="corrective-action"></a>Azione correttiva  
 La proprietà delle regole di confronto del server [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non può essere modificata. Non sarà possibile completare un aggiornamento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sarà necessario eseguire la migrazione dell'installazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un nuovo server che sta utilizzando regole di confronto del server compatibili. Per ulteriori informazioni, vedere quanto segue:  
  
-   [Eseguire l'aggiornamento e la migrazione di Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Selezione di un confronto di SQL Server](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
