---
title: Dll di traduzione | Microsoft Docs
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
ms.openlocfilehash: 168b7b5ef6f8b88a39dbbb0942cf1520adf261e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086036"
---
# <a name="translation-dlls"></a>DDL di traslazione
L'applicazione e l'origine dati spesso archiviano i dati in set di caratteri diversi. ODBC fornisce un meccanismo generico che consente al driver di tradurre i dati da un set di caratteri a un altro. È costituito da una DLL che implementa le funzioni di conversione **SQLDriverToDataSource** e **SQLDataSourceToDriver**, che vengono chiamate dal driver per tradurre tutti i flussi di dati tra l'origine dati e il driver. Questa DLL può essere scritta dallo sviluppatore di applicazioni, dallo sviluppatore del driver o da terze parti.  
  
 È possibile specificare la DLL di traduzione per una determinata origine dati nelle informazioni di sistema per l'origine dati. per altre informazioni, vedere [sottochiavi di specifica dell'origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md). Può anche essere impostata in fase di esecuzione con gli attributi di connessione SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION.  
  
 L'opzione Translation è un valore che può essere interpretato solo da una particolare DLL di traduzione. Se, ad esempio, la DLL di traduzione si traduce tra tabelle codici diverse, l'opzione potrebbe fornire il numero delle tabelle codici utilizzate dall'applicazione e dall'origine dati. Non è necessario che una DLL di conversione usi un'opzione di conversione.  
  
 Dopo aver specificato una DLL di traduzione, il driver la carica e la chiama per tradurre tutti i flussi di dati tra l'applicazione e l'origine dati. Sono incluse tutte le istruzioni SQL e i parametri di tipo carattere inviati all'origine dati e tutti i risultati dei caratteri, come i nomi di colonna e i messaggi di errore recuperati dall'origine dati. I dati di connessione non vengono tradotti, perché la DLL di traduzione non viene caricata finché l'applicazione non si connette all'origine dati.
