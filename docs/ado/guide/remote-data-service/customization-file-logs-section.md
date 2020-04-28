---
title: Sezione log file di personalizzazione | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922781"
---
# <a name="customization-file-logs-section"></a>Sezione Logs del file di personalizzazione
La sezione **logs** contiene una voce del file di log che specifica il nome di un file che registra errori durante il funzionamento della **DataFactory**.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 Una voce del file di log ha il formato seguente:  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>Osservazioni  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**Err**|Stringa letterale che indica che si tratta di una voce del file di log.|  
|*FileName*|Percorso completo e nome file. Il nome file tipico è **c:\msdfmap.log**.|  
  
 Il file di log conterrà il nome utente, HRESULT, data e ora di ogni errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione connessione file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione SQL del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sezione utenti del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni client obbligatorie](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


