---
title: Connessione alle origini dati | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925791"
---
# <a name="connecting-to-data-sources"></a>Connessione a origini dati
Un oggetto **connessione** ADO rappresenta una sessione univoca con un'origine dati, tra cui un DBMS, un archivio di file o un file di testo delimitato da virgole. Nel caso di un sistema di database client/server, la connessione ADO può essere una connessione di rete effettiva al server.  
  
 L'oggetto **Connection** supporta varie [proprietà e metodi](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) per specificare le configurazioni di connessione, aprire e chiudere le connessioni, creare ed eseguire comandi sull'origine dati e fornire informazioni sulla progettazione dell'origine dati sottostante sotto forma di set di righe dello schema e così via. A seconda della funzionalità supportata dal provider, alcune raccolte, metodi o proprietà di un oggetto **connessione** potrebbero non essere disponibili.  
  
 È possibile connettersi a un'origine dati utilizzando un oggetto **connessione** o un oggetto **Recordset** .  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Uso di un oggetto Connection](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Uso di un oggetto Recordset](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Creazione di una stringa di connessione](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Specifica delle proprietà di connessione](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Controllo delle transazioni](../../../ado/guide/data/controlling-transactions-ado.md)
