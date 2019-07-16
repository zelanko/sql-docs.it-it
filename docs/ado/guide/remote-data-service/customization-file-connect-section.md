---
title: Sezione sulla connessione del File di personalizzazione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1de3710590cf49de30ff8e79a6ff829b124c42dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922801"
---
# <a name="customization-file-connect-section"></a>Sezione sulla connessione del file di personalizzazione
Il comportamento predefinito del gestore consiste nel rifiutare tutte le connessioni. Il **connettere** sezione specifica le eccezioni a tale comportamento. Ad esempio, se tutti i **connettere** sezioni sono assenti o vuota, quindi per impostazione predefinita è stato possibile stabilire alcuna connessione.  
  
 Il **connettere** sezione può contenere:  
  
-   Una voce di accesso predefinita che specifica il valore predefinito leggono e scrivono le operazioni consentite sulla connessione. Se è presente alcuna voce di accesso predefinito nella sezione, è possibile che la sezione verrà ignorata.  
  
-   Nuova stringa di connessione che sostituisce la stringa di connessione client.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 Una voce di accesso predefinito è nel formato:  
  
```console
  
Access=  
accessRight  
  
```  
  
 Una voce della stringa di connessione sostituzione è nel formato:  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Note  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**Connect**|Una valore letterale stringa che indica che si è una voce della stringa di connessione.|  
|**_connectionString_**|Stringa che sostituisce la stringa di connessione client intero.|  
|**Accesso**|Una valore letterale stringa che indica che si è una voce di accesso.|  
|**_accessRight_**|Uno dei seguenti diritti di accesso:<br /><br /> -   **NoAccess** -utente non è possibile accedere all'origine dati.<br />-   **ReadOnly** -l'utente può leggere l'origine dati.<br />-   **Lettura/scrittura** -utente può leggere o scrivere nell'origine dati.|  
  
 Se si desidera consentire le connessioni (in disabilitando il comportamento del gestore predefinito), impostare la voce di accesso **connessione predefinita** sezione `Access=ReadWrite`ed eliminare o qualsiasi altro commento **connettersi** _identificatore_ sezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione Log File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione SQL del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sezione UserList del File personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni Client richieste](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione.](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



