---
title: DLL di traduzione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dad12bcd71434c1013b4fde5b4bd0231e56016f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297946"
---
# <a name="translation-dlls"></a>DDL di traslazione
L'applicazione e l'origine dati spesso archiviano i dati in set di caratteri diversi. ODBC fornisce un meccanismo generico che consente al driver di convertire i dati da un set di caratteri a un altro. È costituito da una DLL che implementa le funzioni di conversione **SQLDriverToDataSource** e **SQLDataSourceToDriver**, chiamate dal driver per convertire tutti i dati che passano tra l'origine dati e il driver. Questa DLL può essere scritta dallo sviluppatore dell'applicazione, dallo sviluppatore del driver o da una terza parte.  
  
 La DLL di conversione per una determinata origine dati può essere specificata nelle informazioni di sistema per tale origine dati. Per ulteriori informazioni, consultate [Sottochiavi di specifica dell'origine dati.](../../../odbc/reference/install/data-source-specification-subkeys.md) Può anche essere impostato in fase di esecuzione con gli SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION gli attributi di connessione.  
  
 L'opzione di conversione è un valore che può essere interpretato solo da una particolare DLL di conversione. Ad esempio, se la DLL di conversione viene convertita tra tabelle codici diverse, l'opzione potrebbe fornire il numero delle tabelle codici utilizzate dall'applicazione e dall'origine dati. Non è necessario che una DLL di conversione utilizzi un'opzione di conversione.  
  
 Dopo aver specificato una DLL di conversione, il driver la carica e la chiama per convertire tutti i dati che scorrono tra l'applicazione e l'origine dati. Sono incluse tutte le istruzioni SQL e i parametri di carattere inviati all'origine dati e tutti i risultati dei caratteri, i metadati dei caratteri, ad esempio i nomi delle colonne e i messaggi di errore recuperati dall'origine dati. I dati di connessione non vengono convertiti, perché la DLL di conversione non viene caricata fino a quando l'applicazione si è connessa all'origine dati.
