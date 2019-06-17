---
title: Sezione SQL del File di personalizzazione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba0d8c7ab1294400c19456abf164c6ad6be0dd2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704302"
---
# <a name="customization-file-sql-section"></a>Sezione SQL del file di personalizzazione
Il **sql** sezione può contenere una nuova stringa SQL che sostituisce la stringa di comando di client. Se non è presente alcuna stringa SQL nella sezione, è possibile che la sezione verrà ignorata.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 La nuova stringa SQL può essere *con parametri*. Ovvero i parametri nel **sql** sezione stringa SQL (designato dal '?' caratteri) possono essere sostituiti dagli argomenti corrispondenti in un *identificatore* nella stringa di comando di client (designato da un elenco delimitato da parentesi). L'identificatore e l'elenco di argomenti si comportano come una chiamata di funzione.  
  
 Si supponga ad esempio la stringa di comando del client è `"CustomerByID(4)"`, l'intestazione di sezione SQL è `[SQL CustomerByID]`, e la nuova stringa sezione SQL viene `"SELECT * FROM Customers WHERE CustomerID = ?".` verrà generato il gestore dei `"SELECT * FROM Customers WHERE CustomerID = 4"` e usare tale stringa per eseguire query sull'origine dati.  
  
 Se la nuova istruzione SQL è la stringa null (""), quindi la sezione viene ignorata.  
  
 Se la nuova stringa dell'istruzione SQL non è valida, l'esecuzione dell'istruzione avrà esito negativo. Il client parametro viene ignorato. È possibile farlo intenzionalmente per "disattivare" tutti i comandi SQL client specificando:  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintassi  
 Sostituisce la voce della stringa SQL è nel formato:  
  
 **SQL=**    
 ***sqlString***  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**SQL**|Una valore letterale stringa che indica che si è una voce della sezione SQL.|  
|***sqlString***|Stringa SQL che sostituisce la stringa del client.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione sulla connessione del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione Log File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione UserList del File personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni Client richieste](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione.](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


