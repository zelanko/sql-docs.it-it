---
title: Connettersi a DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ab734e93743d3a3158feb16dba044b58e7f48f23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299160"
---
# <a name="connect-to-db2-db2tosql"></a>Connettersi a DB2 (DB2ToSQL)
Usare la **connettersi a DB2** finestra di dialogo per la connessione al database DB2 che si desidera eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **Connetti a DB2**. Se si è già connessa, il comando viene **Riconnetti a DB2**.  
  
## <a name="options"></a>Opzioni  
**Provider**  
Selezionare il provider di accesso ai dati per la connessione al database DB2. I provider disponibili sono il Provider Client DB2 e il Provider OLE DB. Il valore predefinito è DB2 Client Provider.  
  
**Mode**  
Selezionare modalità Standard, TNSNAME o stringa di connessione.  
  
-   In modalità Standard, immettere o selezionare i valori per il provider, nome del server, porta del server, DB2 SID, nome utente e password.  
  
-   Nella modalità TNSNAME è immettere l'identificatore di connect (alias TNS) del database, nome utente e la password di DB2.  
  
-   In modalità stringa di connessione, è fornire una stringa di connessione.  
  
    > [!IMPORTANT]  
    > Non è consigliabile utilizzare la modalità stringa di connessione perché il testo può includere le password, e viene inviato come testo non crittografato.  
  
Il valore predefinito è la modalità Standard.  
  
**Nome server**  
Immettere il nome del server DB2. Il nome del server predefinita è lo stesso nome del computer. Questa è un'opzione di modalità Standard.  
  
**Porta server**  
Se si usa un numero di porta diverso da 1521 (impostazione predefinita) per le connessioni a DB2, immettere il numero di porta. Questa è un'opzione di modalità Standard.  
  
**Identificatore di connessione**  
Immettere il DB2 connect identificatore. Questo è l'alias del database come definito nel file tnsnames. ora locale.  
  
Questa è un'opzione di modalità TNSNAME.  
  
**DB2 SID**  
Immettere il SID per il database. Il SID è un identificatore che distingue i database di DB2 in un computer. Il valore predefinito di SID per un database è i primi otto caratteri del nome del database.  
  
Questa è un'opzione di modalità Standard.  
  
**Nome utente**  
Immettere il nome utente che SSMA userà per connettersi al database DB2.  
  
**Password**  
Immettere la password associata al nome utente.  
  
**Stringa di connessione**  
> [!IMPORTANT]  
> Non è consigliabile utilizzare la modalità stringa di connessione perché il testo può includere le password, e viene inviato come testo non crittografato.  
  
Se si usa la modalità stringa di connessione, immettere la stringa di connessione completa per la connessione a DB2.  
  
Le stringhe di connessione sono costituiti da coppie nome / valore di parametro.  
  
-   Per informazioni sulla stringa di connessione OLE DB, vedere [Provider Microsoft OLE DB per DB2](https://go.microsoft.com/fwlink/?LinkId=85640) articolo in MSDN Library.  
  
Per le stringhe di connessione di SSMA, sempre includere il parametro del Provider. Inoltre, assicurarsi di includere il parametro Port quando ci si connette a DB2.  
  
