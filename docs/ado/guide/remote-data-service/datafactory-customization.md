---
title: Personalizzazione di DataFactory | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922775"
---
# <a name="datafactory-customization"></a>Personalizzazione di Data Factory
Servizio dati remoto (RDS) fornisce un modo per eseguire facilmente l'accesso ai dati in un sistema a tre livelli client/server. Un controllo client di dati specifica i parametri della stringa di connessione e comando per eseguire una query su un'origine dati remota o stringa di connessione e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) parametri per eseguire un aggiornamento dell'oggetto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 I parametri vengono passati a un'applicazione server, che esegue l'operazione di accesso ai dati nell'origine dati remota. Servizi Desktop remoto offre un programma server predefinito denominato il [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto. Il **RDSServer** oggetto restituisce qualsiasi **Recordset** oggetto generato da una query al client.  
  
 Tuttavia, il **RDSServer** è limitato all'esecuzione di query e aggiornamenti. Non può eseguire qualsiasi convalida o l'elaborazione sulle stringhe di connessione o un comando.  
  
 Con ADO, è possibile specificare che il **DataFactory** funzionano in combinazione con un altro tipo di programma server chiamato un' *gestore*. Il gestore può modificare stringhe di comando e di connessione client prima che vengano utilizzate per accedere all'origine dati. Inoltre, il gestore di è possibile applicare diritti di accesso, che regolano la capacità del client di leggere e scrivere dati nell'origine dati.  
  
 I parametri che il gestore Usa per modificare i parametri del client e i diritti di accesso sono specificati nelle sezioni di un file di personalizzazione.  
  
 Gli argomenti seguenti forniscono altre informazioni sulla personalizzazione il **DataFactory** oggetto.  
  
-   [Informazioni sul file di personalizzazione](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Sezione sulla connessione del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Sezione SQL del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Sezione UserList del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Sezione Logs del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Impostazioni obbligatorie dei client](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


