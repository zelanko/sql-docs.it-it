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
ms.openlocfilehash: 8c4652a3228bb3fb1407a67680e347f6b23a097b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727504"
---
# <a name="mssqlserver_845"></a>MSSQLSERVER_845
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|845|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|BUFLATCH_TIMEOUT|  
|Testo del messaggio|Timeout durante l'attesa di un latch del buffer di tipo %d per la pagina %S_PGID, ID di database %d.|  
  
## <a name="explanation"></a>Spiegazione  
Un processo era in attesa di acquisire un latch, ma ha attesto fino al tempo limite e non ha potuto acquisirne uno. Ciò può verificarsi se il completamento di un'operazione di I/O richiede una quantità di tempo eccessiva, in genere a causa di un blocco dei processi di sistema determinato da altre attività. In alcuni casi, tuttavia, può essere dovuto a un errore hardware.  
  
## <a name="user-action"></a>Azione dell'utente  
È possibile impedire che si verifichi questo errore eseguendo le attività seguenti:  
  
-   Ridurre il carico di lavoro.  
  
-   Verificare se sono presenti errori di I/O associati nel log degli errori o nel log eventi. Gli errori di I/O sono in genere causati da un malfunzionamento del disco.  
  
-   Verificare nel log degli errori se sono presenti attività che non cedono il controllo e altri errori critici.  
  
-   Se si verificano spesso errori critici, ad esempio di asserzione, risolvere tali problemi.  
  
Se l'errore persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.  
  
