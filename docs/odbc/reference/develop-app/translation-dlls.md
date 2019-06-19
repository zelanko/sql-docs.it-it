---
title: DLL di conversione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1d0e23019f3e5b68ad38711c1f041b160ceb31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305738"
---
# <a name="translation-dlls"></a>DDL di traslazione
L'applicazione e l'origine dati spesso archiviano i dati in set di caratteri diversi. ODBC fornisce un meccanismo generico che consente al driver di convertire i dati da un set di caratteri da un altro. È costituito da una DLL che implementa le funzioni di conversione **SQLDriverToDataSource** e **SQLDataSourceToDriver**, che vengono chiamati dal driver per convertire tutti i dati trasmessi tra l'origine dati e il driver. Questa DLL può essere scritto dallo sviluppatore dell'applicazione, lo sviluppatore, driver o di terze parti.  
  
 La DLL di conversione per una determinata origine dati può essere specificato nelle informazioni di sistema per l'origine dati; per altre informazioni, vedere [sottochiavi di specifica origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md). È possibile impostarla anche in fase di esecuzione con gli attributi di connessione SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION.  
  
 L'opzione di conversione è un valore che può essere interpretato solo da una DLL di conversione specifico. Ad esempio, se la traduzione DLL esegue la conversione tra tabelle codici diverse, l'opzione possibile assegnare i numeri delle tabelle codici utilizzate dall'applicazione e l'origine dati. Non è necessario per una DLL di conversione per usare un'opzione di conversione.  
  
 Dopo la conversione che DLL è stata specificata, il driver lo carica e lo chiama per convertire tutti i dati trasmessi tra l'applicazione e l'origine dati. Questo include tutte le istruzioni SQL e i parametri di tipo carattere inviati all'origine dati e tutti i risultati di carattere, i metadati di carattere, ad esempio nomi di colonna e i messaggi di errore recuperati dall'origine dati. Dati di connessione non viene convertiti, poiché la DLL di conversione non viene caricata fino a dopo che l'applicazione è connesso all'origine dati.
