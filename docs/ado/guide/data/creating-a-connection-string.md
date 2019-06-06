---
title: Creazione di una stringa di connessione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ed1a2ec745b1e1ca961c71c81d44ff659789efea
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700867"
---
# <a name="creating-a-connection-string"></a>Creazione di una stringa di connessione
Una stringa di connessione è costituita da un elenco di coppie valore/argomento (vale a dire, parametri), separato da punti e virgola. Ad esempio:  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 Tutti i parametri devono essere riconosciuti da ADO o il provider specificato.  
  
 ADO riconosce i seguenti cinque argomenti in una stringa di connessione.  
  
|Argomento|Descrizione|  
|--------------|-----------------|  
|*Provider*|Specifica il nome di un provider da utilizzare per la connessione.|  
|*Nome file*|Specifica il nome di un file specifico del provider (ad esempio, un oggetto origine dati persistenti) che contiene informazioni di connessione predefinite.|  
|*URL*|Specifica la stringa di connessione come un URL assoluto che identifica una risorsa, ad esempio un file o directory.|  
|*Provider remoto*|Specifica il nome di un provider da utilizzare quando si apre una connessione client-side. (Solo servizio dati remoto).|  
|*Server remoto*|Specifica il nome del percorso del server da usare quando si apre una connessione client-side. (Solo servizio dati remoto).|  
  
 Altri argomenti vengono passati al provider denominato nel *Provider* argomento, senza alcuna elaborazione da parte di ADO.  
  
 L'applicazione di HelloData in [HelloData: Un'applicazione semplice ADO](../../../ado/guide/data/hellodata-a-simple-ado-application.md) usata la stringa di connessione seguente:  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 In questa stringa di connessione ADO riconosce solo il `"Provider=SQLOLEDB"` parametro che specifica il Provider Microsoft OLE DB per SQL Server come origine dati ADO. Il resto delle coppie di valore dell'argomento /, `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`, vengono passati verbatim per questo provider. Il tipo e la validità di tali parametri sono specifici del provider. Per informazioni sui parametri validi che può essere passato nella stringa di connessione, consultare la documentazione del provider singoli.  
  
 Secondo il Provider OLE DB per la documentazione di SQL Server, è possibile sostituire "Server" per il *Zdroj dat* parametro e "Database" per il *Initial Catalog* parametro. Di conseguenza, la stringa di connessione seguente produrrà risultati identici a quello riportato sopra:  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
