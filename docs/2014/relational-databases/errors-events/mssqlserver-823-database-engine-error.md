---
title: MSSQLSERVER_823 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7ece8314c37546b29ab27451a75d2a1866aebc30
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59936508"
---
# <a name="mssqlserver823"></a>MSSQLSERVER_823
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|823|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|B_HARDERR|  
|Testo del messaggio|Il sistema operativo ha restituito l'errore %ls a SQL Server durante un'operazione %S_MSG, all'offset %#016I64x nel file '%ls'. Per informazioni più dettagliate, vedere i messaggi aggiuntivi nel log degli errori di SQL Server e nel registro eventi di sistema. Si tratta di una condizione di errore grave a livello di sistema, che può compromettere l'integrità del database e deve essere corretta immediatamente. Eseguire un controllo di consistenza completo del database (DBCC CHECKDB). L'errore può essere causato da molti fattori. Per ulteriori informazioni, vedere la documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
 Una richiesta di lettura o scrittura di Windows non è stata eseguita. Il messaggio include il codice di errore restituito da Windows e il testo corrispondente. Nel caso di una richiesta di lettura, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono eseguiti quattro tentativi prima di generare il messaggio. Il problema è spesso dovuto a un errore hardware, ma può essere causato dal driver del dispositivo. Per altre informazioni sull'errore 823, vedere [https://support.microsoft.com/kb/828339](https://support.microsoft.com/kb/828339). Per altre informazioni sugli errori di I/O, vedere il capitolo 2 della pagina relativa alle [nozioni fondamentali sull'I/O in Microsoft SQL Server](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)).  
  
## <a name="user-action"></a>Azione dell'utente  
 Per ulteriori informazioni vedere il registro eventi di sistema. Contattare il produttore dell'hardware o il Servizio Supporto Tecnico Clienti Microsoft per determinare la causa e l'azione di correzione appropriata. Dopo la correzione dell'errore hardware, ripristinare tutti i database ed eseguire DBCC CHECKDB.  
  
  
