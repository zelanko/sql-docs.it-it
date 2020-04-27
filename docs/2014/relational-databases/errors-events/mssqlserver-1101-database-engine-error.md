---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d4468e85f8170ecb6b23abf5af8ee3a114a6bef3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870169"
---
# <a name="mssqlserver_1101"></a>MSSQLSERVER_1101
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1101|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NOALLOCPG|  
|Testo del messaggio|Impossibile allocare una nuova pagina per il database '%.*ls' a causa di spazio su disco insufficiente nel filegroup '%.\*ls'. Liberare lo spazio necessario eliminando oggetti dal filegroup, aggiungendo file al filegroup oppure attivando l'aumento automatico delle dimensioni per i file esistenti nel filegroup.|  
  
## <a name="explanation"></a>Spiegazione  
 Nel filegroup indicato non vi è spazio disponibile su disco.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire le azioni seguenti per tentare di liberare spazio sufficiente nel filegroup.  
  
-   Attivare l'aumento automatico delle dimensioni dei file.  
  
-   Aggiungere altri file al gruppo di file.  
  
-   Liberare spazio su disco eliminando indici o tabelle non necessari dal filegroup.  
  
  
