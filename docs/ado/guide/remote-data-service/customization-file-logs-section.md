---
title: Sezione Logs del File di personalizzazione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14c5436478444e525c7a9753cf3e4e5cddb92f5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922781"
---
# <a name="customization-file-logs-section"></a>Sezione Logs del file di personalizzazione
Il **registri** sezione contiene una voce di file di log, che specifica il nome di un file che registra gli errori durante l'operazione del **DataFactory**.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 Una voce di file di log è nel formato:  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>Note  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**err**|Una valore letterale stringa che indica che si è una voce di file di log.|  
|*FileName*|Un nome file e percorso completo. Il nome di file è **c:\msdfmap.log**.|  
  
 Il file di log conterrà il nome utente, HRESULT, data e ora di ogni errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione sulla connessione del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione SQL del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sezione UserList del File personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni Client richieste](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione.](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


