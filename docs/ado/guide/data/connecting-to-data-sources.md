---
title: Connessione a origini dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 000302715e7ce7d3a8ae53f06d61f54e98cbd883
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925791"
---
# <a name="connecting-to-data-sources"></a>Connessione a origini dati
Un oggetto ADO **connessione** oggetto rappresenta una sessione univoca con un'origine dati, inclusi un DBMS, un archivio di file o un file di testo delimitato da virgole. Nel caso di un sistema di database client/server, la connessione di ADO può essere una connessione di rete effettivo al server.  
  
 Il **Connection** oggetto supporta vari [proprietà e metodi](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) per specificare le configurazioni delle connessioni, apertura e chiusura delle connessioni, la creazione e l'esecuzione di comandi sull'origine dati e fornire informazioni sulla progettazione dell'origine dati sottostante sotto forma di set di righe dello schema, e così via. A seconda delle funzionalità supportate dal provider, alcune raccolte, metodi o proprietà di un **connessione** oggetto potrebbe non essere disponibile.  
  
 È possibile connettersi a un'origine dati tramite un **Connection** dell'oggetto o usando un **Recordset** oggetto.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Uso di un oggetto Connection](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Uso di un oggetto Recordset](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Creazione di una stringa di connessione](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Specificazione delle proprietà della connessione](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Controllo delle transazioni](../../../ado/guide/data/controlling-transactions-ado.md)
