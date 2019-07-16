---
title: Utilizzo di origini dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951809"
---
# <a name="using-data-sources"></a>Uso delle origini dati
Origini dati vengono in genere create dall'utente finale o un riferimento con un programma denominato il *Amministratore ODBC*. L'amministratore ODBC richiede all'utente per il driver da usare e quindi chiama tale driver. Il driver consente di visualizzare una finestra di dialogo che richiede le informazioni che necessarie per connettersi all'origine dati. Dopo che l'utente immette le informazioni, il driver viene archiviato nel sistema.  
  
 In un secondo momento, l'applicazione chiama il responsabile del Driver e lo passa il nome di un'origine dati di computer o il percorso di un file contenente un'origine dati file. Se viene passato un nome computer dell'origine dati, gestione Driver Cerca il sistema per trovare il driver utilizzato dall'origine dati. Quindi carica il driver e passa il nome dell'origine dati a esso. Il driver Usa il nome dell'origine dati per trovare le informazioni che necessarie per connettersi all'origine dati. Infine, si connette all'origine dati, in genere chiedere conferma all'utente per un ID utente e una password che non sono in genere archiviate.  
  
 Se viene passato a un'origine dati file, gestione Driver apre il file e carica il driver specificato. Se il file contiene anche una stringa di connessione, questo passa al driver. Utilizzando le informazioni nella stringa di connessione, il driver si connette all'origine dati. Se nessuna stringa di connessione è stata passata, il driver in genere richiede all'utente le informazioni necessarie.
