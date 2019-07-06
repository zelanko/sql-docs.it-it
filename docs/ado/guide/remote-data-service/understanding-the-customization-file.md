---
title: Informazioni sul file di personalizzazione. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d58edcfae92c94cfc635d3539f81faf834e382c7
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597566"
---
# <a name="understanding-the-customization-file"></a>Informazioni sul file di personalizzazione
Ogni intestazione di sezione nel file di personalizzazione è costituito da parentesi quadre ( **[]** ) che contiene un tipo e un parametro. Per le stringhe letterali sono indicati i quattro tipi di sezioni **connettersi**, **sql**, **elencoutenti**, oppure **log**. Il parametro è la stringa letterale, il valore predefinito, un identificatore specificato dall'utente o nulla.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Pertanto, ogni sezione è contrassegnata con una delle intestazioni delle sezioni seguenti:  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Intestazioni delle sezioni sono le parti seguenti.  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**connect**|Una stringa letterale che modifica la stringa di connessione.|  
|**sql**|Una stringa letterale che modifica una stringa di comando.|  
|**userlist**|Una stringa letterale che modifica i diritti di accesso di un utente specifico.|  
|**logs**|Valore letterale stringa che specifica un file di log di registrazione errori operativi.|  
|**default**|Una stringa letterale che viene usata se è specificato o è disponibile alcun identificatore.|  
|*identifier*|Stringa che corrisponde a una stringa nel **connettersi** oppure **comando** stringa.<br /><br /> -Usare questa sezione se contiene l'intestazione della sezione **connettere** e la stringa dell'identificatore è presente nella stringa di connessione.<br />-Usare questa sezione se contiene l'intestazione della sezione **sql** e la stringa dell'identificatore è presente nella stringa di comando.<br />-Usare questa sezione se contiene l'intestazione della sezione **userlist** e la stringa dell'identificatore corrisponde a un **connettersi** identificatore di sezione.|  
  
 Il **DataFactory** chiama il gestore, passando i parametri di client. Il gestore di ricerca intere stringhe nei parametri del client che corrispondono a identificatori nelle intestazioni di sezione appropriata. Se viene trovata una corrispondenza, il contenuto della sezione viene applicato al parametro del client.  
  
 Una sezione viene usata nelle circostanze seguenti:  
  
-   Oggetto **connettersi** sezione viene usata se la parte valore del client di connettersi, parola chiave della stringa "**origine dati =** _valore_", corrisponde a un **connettersi** Identificatore di sezione. 
  
-   Un' **sql** sezione viene usata se la stringa di comando del client contiene una stringa che corrisponde a un **sql** identificatore di sezione.  
  
-   Oggetto **connettersi** oppure **sql** sezione con un parametro predefinito viene usato se non vi è alcun identificatore corrispondente.  
  
-   Oggetto **elencoutenti** sezione viene usata se il **elencoutenti** sezione identificatore corrisponde a una **connettersi** identificatore di sezione. Se non esiste una corrispondenza, il contenuto del **elencoutenti** sezione vengono applicate per la connessione disciplinata dalle **connettersi** sezione.  
  
-   Se la stringa in una stringa di connessione o un comando non corrisponde l'identificatore in qualsiasi **connettersi** oppure **sql** intestazione della sezione e non esiste alcun **connettersi** o **sql**  sezione intestazione con un parametro predefinito, la stringa del client viene usato senza alcuna modifica.  
  
-   Il **registri** sezione viene utilizzata ogni volta che il **DataFactory** è in esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione sulla connessione del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione Log File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione SQL del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sezione UserList del File personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni Client richieste](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

