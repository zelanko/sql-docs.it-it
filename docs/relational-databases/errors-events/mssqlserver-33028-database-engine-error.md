---
description: MSSQLSERVER_33028
title: MSSQLSERVER_33028 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 83c7c1bcd4531ccd4dc1e0eb37876c6ed82d031b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460946"
---
# <a name="mssqlserver_33028"></a>MSSQLSERVER_33028
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|33028|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SEC_CRYPTOPROV_CANTOPENSESSION|  
|Testo del messaggio|Impossibile aprire la sessione per % S_MSG '%.* ls.' Codice di errore del provider: %d.|  
  
## <a name="explanation"></a>Spiegazione  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è stato in grado di aprire il provider del servizio di crittografia elencato nel messaggio di errore. Il codice di errore è stato indicato dal provider del servizio di crittografia. Per ulteriori informazioni sull'errore, potrebbe essere necessario contattare il provider.  
  
|Codice di errore|Descrizione|  
|--------------|---------------|  
|0|Esito positivo. Nessun errore.|  
|1|Esito negativo. Si verificato un errore non specificato o imprevisto. Non sono disponibili informazioni aggiuntive.|  
|2|Buffer insufficiente. Impossibile allocare lo spazio per il provider del servizio di crittografia.|  
|3|Non supportato. Il provider di crittografia non è supportato da questa versione. Selezionare un altro provider del servizio di crittografia.|  
|4|Non trovato. Il provider del servizio di crittografia specificato non è presente o non si dispone dell'autorizzazione per accedere ai file.|  
|5|Errore di autorizzazione. Viene visualizzato se si specifica una password o un nome utente errati durante la creazione della credenziale o quando la credenziale non esiste.|  
|6|Argomento non valido. Un argomento non valido è stato passato al provider del servizio di crittografia.|  
  
## <a name="user-action"></a>Azione dell'utente  
Risolvere l'errore o contattare il provider del servizio di crittografia per ulteriori informazioni.  
  
