---
title: Personalizzazione di datafactory | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bdc406778bea0d6355e747998d2517b841fc17b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922775"
---
# <a name="datafactory-customization"></a>Personalizzazione di Data Factory
Remote Data Service (RDS) fornisce un modo per eseguire facilmente l'accesso ai dati in un sistema client/server a tre livelli. Un controllo dati client specifica la connessione e i parametri della stringa di comando per eseguire una query su un'origine dati remota, oppure su una stringa di connessione e parametri dell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per eseguire un aggiornamento.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 I parametri vengono passati a un programma server che esegue l'operazione di accesso ai dati nell'origine dati remota. RDS fornisce un programma server predefinito denominato oggetto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) . L'oggetto **RDSServer. DataFactory** restituisce al client qualsiasi oggetto **Recordset** prodotto da una query.  
  
 Tuttavia, **RDSServer. DataFactory** è limitato all'esecuzione di query e aggiornamenti. Non può eseguire alcuna convalida o elaborazione sulla connessione o sulle stringhe di comando.  
  
 Con ADO è possibile specificare che la **DataFactory** funzioni insieme a un altro tipo di programma server chiamato *gestore*. Il gestore può modificare la connessione client e le stringhe di comando prima che vengano utilizzate per accedere all'origine dati. Inoltre, il gestore può applicare i diritti di accesso, che regolano la capacità del client di leggere e scrivere i dati nell'origine dati.  
  
 I parametri utilizzati dal gestore per modificare i parametri client e i diritti di accesso vengono specificati nelle sezioni di un file di personalizzazione.  
  
 Negli argomenti seguenti vengono fornite ulteriori informazioni sulla personalizzazione dell'oggetto **DataFactory** .  
  
-   [Informazioni sul file di personalizzazione](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Sezione sulla connessione del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Sezione SQL del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Sezione UserList del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Sezione Logs del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Impostazioni obbligatorie dei client](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


