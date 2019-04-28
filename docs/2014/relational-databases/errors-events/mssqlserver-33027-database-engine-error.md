---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 751b3615e8c54ab5899f64a6604c5a228c859879
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868687"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|33027|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Testo del messaggio|Impossibile caricare il provider del servizio di crittografia '%.*ls' a causa di una firma Authenticode o un percorso file non valido. Controllare i messaggi precedenti per altri errori.|  
  
## <a name="explanation"></a>Spiegazione  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è stato in grado di usare il provider del servizio di crittografia elencato nel messaggio di errore perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di caricare la DLL. Il nome non è valido o la firma Authenticode è non valida.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che il file sia presente e che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponga dell'autorizzazione ad accedere a tale percorso. Per visualizzare altri messaggi correlati, controllare il log degli errori. In caso contrario, contattare il provider del servizio di crittografia per ulteriori informazioni.  
  
  
