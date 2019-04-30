---
title: Connettersi a Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0805246d5b88138cfa97019d1e0cd524c82456c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061004"
---
# <a name="connect-to-sybase-sybasetosql"></a>Connettersi a Sybase (SybaseToSQL)
Usare la **connettersi a Sybase** finestra di dialogo per connettersi all'istanza di Sybase Adaptive Server Enterprise (ASE) che si desidera eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **Connetti a Sybase**. Se si è già connessa, il comando viene **Riconnetti a Sybase**.  
  
## <a name="options"></a>Opzioni  
**Provider**  
Selezionare una qualsiasi del Provider installato nel computer per la connessione al Sybase Server.  
  
**Mode**  
Selezionare entrambe le modalità di connessione standard o avanzata. In modalità standard, immettere o selezionare i valori per il nome del server, porta, nome utente e password. Nella modalità avanzata è fornire una stringa di connessione.  
  
**Nome server**  
Immettere o selezionare il nome o indirizzo IP del Server adattivo. Il nome del server predefinita è lo stesso nome del computer. Questa è un'opzione di modalità standard.  
  
**Porta server**  
Se si usa una porta non predefiniti per le connessioni ad ambiente del servizio App, immettere il numero di porta. Il numero di porta predefinito è 5000. Questa è un'opzione di modalità standard.  
  
**Nome utente**  
Immettere il nome utente usato per connettersi all'ambiente del servizio app. Questa è un'opzione di modalità standard.  
  
**Password**  
Immettere la password associata al nome utente. Questa è un'opzione di modalità standard.  
  
**Stringa di connessione**  
Immettere la stringa di connessione completa per la connessione per l'ambiente del servizio app.  
  
Le stringhe di connessione sono costituiti da coppie nome / valore di parametro. I nomi dei parametri variano con il provider in uso.  
  
**Come indicato di seguito sono riportati i parametri di connessione per diversi provider:**  
  
1.  Parametri di connessione per **Provider OLE DB**  
  
    |Impostazione|Parametro Sybase 12,5|Parametro Sybase 15|  
    |-----------|-------------------------|-----------------------|  
    |Nome server|Server Name|Server|  
    |Port|Indirizzo di porta del server|Port|  
    |Nome utente|ID utente|ID utente|  
    |Password|Password|Password|  
    |Provider|Provider|Provider|  
  
    Per Sybase ASE 12,5, una stringa di connessione di esempio è il seguente:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Per Sybase ASE 15, una stringa di connessione di esempio è il seguente:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Parametri di connessione per **Provider ODBC**  
  
    |Impostazione|Parametro Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nome del driver|Driver|  
    |Server Name|Server|  
    |Nome utente|Uid|  
    |Password|Pwd|  
    |Numero di porta|Port|  
  
    Per Sybase ASE 12,5 o 15, una stringa di connessione di esempio è il seguente:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Parametri di connessione per **Provider ADO.NET**  
  
    |Impostazione|Parametro Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Server Name|Server|  
    |Nome utente|Uid|  
    |Password|Pwd|  
    |Numero di porta|Port|  
  
    Un esempio della stringa di connessione per il Provider ADO.NET è i seguenti:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Per altre informazioni, vedere la documentazione di ambiente del servizio app.  
  
Si tratta di un'opzione di modalità avanzata.  
  
