---
title: Connettersi a Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 42ab1e77dbdb7cee237a9ec22c49a725a64390c0
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264477"
---
# <a name="connect-to-oracle-oracletosql"></a>Connettersi a Oracle (OracleToSQL)
Usare la **Connetti a Oracle** finestra di dialogo per la connessione al database Oracle che vuoi eseguire la migrazione.  
  
Per accedere a questa finestra di dialogo, scegliere il **File** dal menu **Connect to Oracle**. Se si è già connessa, il comando viene **Riconnetti a Oracle**.  
  
## <a name="options"></a>Opzioni  
**Provider**  
Selezionare il provider di accesso ai dati per la connessione al database Oracle. I provider disponibili sono il Provider del Client Oracle e il Provider OLE DB. Il valore predefinito è Provider Client Oracle.  
  
**Mode**  
Selezionare modalità Standard, TNSNAME o stringa di connessione.  
  
-   In modalità Standard, immettere o selezionare i valori per il provider, nome del server, porta del server, Oracle SID, nome utente e password.  
  
-   In modalità TNSNAME, immettere l'identificatore di connect (alias TNS) del database Oracle, nome utente e password.  
  
-   In modalità stringa di connessione, è fornire una stringa di connessione.  
  
    > [!IMPORTANT]  
    > Non è consigliabile utilizzare la modalità stringa di connessione perché il testo può includere le password, e viene inviato come testo non crittografato.  
  
Il valore predefinito è la modalità Standard.  
  
**Nome server**  
Immettere il nome del server Oracle. Il nome del server predefinita è lo stesso nome del computer. Questa è un'opzione di modalità Standard.  
  
**Porta server**  
Se si usa un numero di porta diverso da 1521 (impostazione predefinita) per le connessioni a Oracle, immettere il numero di porta. Questa è un'opzione di modalità Standard.  
  
**Identificatore di connessione**  
Immettere il Oracle connect identificatore. Questo è l'alias del database come definito nel file tnsnames. ora locale.  
  
Questa è un'opzione di modalità TNSNAME.  
  
**SID Oracle**  
Immettere il SID per il database. Il SID è un identificatore che consente di distinguere il database Oracle in un computer. Il valore predefinito di SID per un database è i primi otto caratteri del nome del database.  
  
Questa è un'opzione di modalità Standard.  
  
**Nome utente**  
Immettere il nome utente che SSMA userà per connettersi al database Oracle.  
  
**Password**  
Immettere la password associata al nome utente.  
  
**Stringa di connessione**  
> [!IMPORTANT]  
> Non è consigliabile utilizzare la modalità stringa di connessione perché il testo può includere le password, e viene inviato come testo non crittografato.  
  
Se si usa la modalità stringa di connessione, immettere la stringa di connessione completa per la connessione a Oracle.  
  
Le stringhe di connessione sono costituiti da coppie nome / valore di parametro.  
  
-   Per informazioni sulla stringa di connessione OLE DB, vedere [Provider Microsoft OLE DB per Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) articolo in MSDN Library.  
  
Per le stringhe di connessione di SSMA, sempre includere il parametro del Provider. Inoltre, assicurarsi di includere il parametro Port quando ci si connette a Oracle.  
  
