---
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce297a1c2bc782a82a322618acedb102bb9e18eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101478"
---
# <a name="mssqlserver845"></a>MSSQLSERVER_845
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|845|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|BUFLATCH_TIMEOUT|  
|Testo del messaggio|Timeout durante l'attesa di un latch del buffer di tipo %d per la pagina %S_PGID, ID di database %d.|  
  
## <a name="explanation"></a>Spiegazione  
Un processo in attesa di acquisire un latch non è stato in grado di acquisirne uno prima della scadenza del limite di tempo. Ciò può verificarsi se il completamento di un'operazione di I/O richiede una quantità di tempo eccessiva, in genere a causa di un blocco dei processi di sistema determinato da altre attività. In alcuni casi, tuttavia, può essere dovuto a un errore hardware.  
  
## <a name="user-action"></a>Azione dell'utente  
È possibile impedire che si verifichi questo errore eseguendo le attività seguenti:  
  
-   Ridurre il carico di lavoro.  
  
-   Verificare se sono presenti errori di I/O associati nel log degli errori o nel log eventi. Gli errori di I/O sono in genere causati da un malfunzionamento del disco.  
  
-   Verificare nel log degli errori se sono presenti attività che non cedono il controllo e altri errori critici.  
  
-   Se si verificano spesso errori critici, ad esempio di asserzione, risolvere tali problemi.  
  
Se l'errore persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.  
  
