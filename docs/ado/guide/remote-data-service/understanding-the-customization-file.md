---
title: Informazioni sul file di personalizzazione | Microsoft Docs
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
ms.openlocfilehash: 81a73044c1ab413fb2b49286814f3e6b3951c6c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921966"
---
# <a name="understanding-the-customization-file"></a>Informazioni sul file di personalizzazione
Ogni intestazione di sezione nel file di personalizzazione è costituita da parentesi quadre (**[]**) contenenti un tipo e un parametro. I quattro tipi di sezione sono indicati dalle stringhe letterali **Connect**, **SQL**, **Users**o **logs**. Il parametro è la stringa letterale, l'impostazione predefinita, un identificatore specificato dall'utente o Nothing.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Ogni sezione è quindi contrassegnata con una delle seguenti intestazioni di sezione:  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Le intestazioni della sezione hanno le parti seguenti.  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**connettersi**|Stringa letterale che modifica una stringa di connessione.|  
|**sql**|Stringa letterale che modifica una stringa di comando.|  
|**UserList**|Stringa letterale che modifica i diritti di accesso di un utente specifico.|  
|**log**|Stringa letterale che specifica un file di log che registra errori operativi.|  
|**predefinita**|Stringa letterale utilizzata se non viene specificato o trovato alcun identificatore.|  
|*identificatore*|Stringa che corrisponde a una stringa nella stringa di **connessione** o di **comando** .<br /><br /> -Usare questa sezione se l'intestazione della sezione contiene **Connect** e la stringa dell'identificatore si trova nella stringa di connessione.<br />-Usare questa sezione se l'intestazione della sezione contiene **SQL** e la stringa dell'identificatore si trova nella stringa di comando.<br />-Usare questa sezione se l'intestazione della sezione contiene **Users** e la stringa dell'identificatore corrisponde a un identificatore di sezione **Connect** .|  
  
 **DataFactory** chiama il gestore, passando i parametri client. Il gestore cerca le stringhe intere nei parametri client che corrispondono agli identificatori nelle intestazioni di sezione appropriate. Se viene trovata una corrispondenza, il contenuto della sezione viene applicato al parametro client.  
  
 Una sezione specifica viene utilizzata nelle circostanze seguenti:  
  
-   Una sezione **Connect** viene usata se la parte relativa al valore della parola chiave della stringa di connessione del client, "**Data Source =**_value_", corrisponde a un identificatore di sezione **Connect** . 
  
-   Viene utilizzata una sezione **SQL** se la stringa di comando del client contiene una stringa che corrisponde a un identificatore di sezione **SQL** .  
  
-   Se non esiste un identificatore corrispondente, viene utilizzata una sezione **Connect** o **SQL** con un parametro predefinito.  
  
-   Viene utilizzata una sezione **Users** se l'identificatore della sezione **dell'utente** corrisponde a un identificatore di sezione **Connect** . Se esiste una corrispondenza, il contenuto della sezione dell' **utente** viene applicato alla connessione governata dalla sezione **Connect** .  
  
-   Se la stringa in una connessione o in una stringa di comando non corrisponde all'identificatore in nessuna intestazione della sezione **connessione** o **SQL** e non è presente alcuna intestazione di sezione **Connect** o **SQL** con un parametro predefinito, la stringa client viene utilizzata senza modifiche.  
  
-   La sezione **logs** viene usata ogni volta che la **DataFactory** è in funzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione connessione file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione log file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione SQL del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sezione utenti del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni client obbligatorie](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

