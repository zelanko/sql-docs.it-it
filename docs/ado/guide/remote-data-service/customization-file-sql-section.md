---
title: Sezione SQL del file di personalizzazione | Microsoft Docs
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
ms.openlocfilehash: 6163a5b5fd0999e17e17961639e0a1fee3e8fa4c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922792"
---
# <a name="customization-file-sql-section"></a>Sezione SQL del file di personalizzazione
La sezione **SQL** può contenere una nuova stringa SQL che sostituisce la stringa di comando del client. Se nella sezione non è presente alcuna stringa SQL, la sezione verrà ignorata.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 La nuova stringa SQL può essere *parametrizzata*. Ovvero, i parametri della sezione **SQL** stringa SQL (designata dal carattere "?") possono essere sostituiti dagli argomenti corrispondenti in un *identificatore* nella stringa di comando del client (designato da un elenco delimitato da virgole tra parentesi). L'identificatore e l'elenco di argomenti si comportano come una chiamata di funzione.  
  
 Si supponga, ad esempio, che la stringa `"CustomerByID(4)"`di comando del client sia, `[SQL CustomerByID]`che l'intestazione della sezione SQL sia e `"SELECT * FROM Customers WHERE CustomerID = ?".` che la nuova stringa `"SELECT * FROM Customers WHERE CustomerID = 4"` di sezione SQL sia il gestore a generare e utilizzare tale stringa per eseguire una query sull'origine dati.  
  
 Se la nuova istruzione SQL è la stringa null (""), la sezione verrà ignorata.  
  
 Se la nuova stringa dell'istruzione SQL non è valida, l'esecuzione dell'istruzione avrà esito negativo. Il parametro client viene effettivamente ignorato. Questa operazione può essere eseguita intenzionalmente per disattivare tutti i comandi SQL del client specificando:  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintassi  
 Una voce di stringa SQL sostitutiva ha il formato seguente:  
  
 **SQL =**   
 ***sqlString***  
  
|Parte|Descrizione|  
|----------|-----------------|  
|**SQL**|Stringa letterale che indica che si tratta di una voce di sezione SQL.|  
|***sqlString***|Stringa SQL che sostituisce la stringa del client.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione connessione file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione log file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione utenti del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni client obbligatorie](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


