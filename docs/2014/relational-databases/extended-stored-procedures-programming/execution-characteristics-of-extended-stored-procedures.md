---
title: Caratteristiche dell'esecuzione di Stored procedure estese | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d21f002ca6b7ea185df2e01f66abf0e1ef5cfd1b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765863"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>Caratteristiche dell'esecuzione di stored procedure estese
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 L'esecuzione di una stored procedure estesa presenta tre caratteristiche:  
  
-   La funzione di stored procedure estesa viene eseguita nel contesto di sicurezza del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   La funzione della stored procedure estesa viene eseguita nello spazio di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Il thread associato all'esecuzione della stored procedure estesa è lo stesso utilizzato per la connessione client.  
  
    > [!IMPORTANT]  
    >  Prima di aggiungere stored procedure estese al server e concedere le autorizzazioni di esecuzione ad altri utenti, è necessario che l'amministratore di sistema esamini con attenzione ogni stored procedure estesa per verificare che non contenga codice dannoso o malware.  
  
-  
  
 Dopo che la stored procedure estesa DLL viene caricata, la DLL rimane caricata nello spazio degli indirizzi del server finché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato arrestato o l'amministratore Scarica in modo esplicito la DLL tramite DBCC *Nome_DLL* (gratuito).  
  
 La stored procedure estesa può essere eseguita da [!INCLUDE[tsql](../../includes/tsql-md.md)] come stored procedure mediante l'istruzione EXECUTE:  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>Parametri  
 \@ *retval*  
 È un valore restituito.  
  
 \@ *param1*  
 È un parametro di input.  
  
 \@ *param2*  
 È un parametro di input/output.  
  
> [!CAUTION]  
>  Le stored procedure estese offrono miglioramenti delle prestazioni ed estendono la funzionalità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia dal momento che la DLL della stored procedure estesa e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] condividono lo stesso spazio degli indirizzi, una procedura problematica può compromettere il funzionamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sebbene le eccezioni generate dalla DLL delle stored procedure estese vengano gestite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile danneggiare le aree dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Come precauzione di sicurezza, solo gli amministratori di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono aggiungere stored procedure estese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È consigliabile testare completamente tali procedure prima dell'installazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione di Stored procedure estese](database-engine-extended-stored-procedures-programming.md)   
 [Esecuzione di query su stored procedure estese installate in SQL Server](querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
