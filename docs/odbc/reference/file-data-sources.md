---
description: Origini dati di file
title: Origini dati file | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d02c767adab90ee4a7b6ff93a34886c03b87780c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429043"
---
# <a name="file-data-sources"></a>Origini dati di file
Le *origini dati dei file* vengono archiviate in un file e consentono di usare le informazioni di connessione ripetutamente da un singolo utente o condivise tra più utenti. Quando si utilizza un'origine dati file, gestione driver esegue la connessione all'origine dati utilizzando le informazioni contenute in un file con estensione DSN. Questo file può essere modificato in modo analogo a qualsiasi altro file. Un'origine dati file non dispone di un nome di origine dati, così come un'origine dati del computer, e non è registrata per un utente o un computer.  
  
 Un'origine dati file semplifica il processo di connessione, perché il file con estensione DSN contiene la stringa di connessione che altrimenti sarebbe necessario compilare per una chiamata alla funzione **SQLDriverConnect** . Un altro vantaggio del file con estensione DSN è che è possibile copiarlo in qualsiasi computer, in modo che le origini dati identiche possano essere usate da molti computer, purché dispongano del driver appropriato. Un'origine dati di file può essere condivisa anche dalle applicazioni. Un'origine dati file condivisibile può essere posizionata in una rete e utilizzata simultaneamente da più applicazioni.  
  
 Un file con estensione DSN può inoltre essere non condivisibile. Un file con estensione DSN non condivisibile si trova in un singolo computer e punta a un'origine dati del computer. Le origini dati di file non condivisibili sono prevalentemente per consentire una semplice conversione delle origini dati del computer in origini dati di file in modo che un'applicazione possa essere progettata per funzionare esclusivamente con origini dati di file. Quando Gestione driver invia le informazioni in un'origine dati di file non condivisibile, si connette a seconda dell'origine dati del computer a cui punta il file con estensione DSN.  
  
 Per ulteriori informazioni sulle origini dati dei file, vedere [connessione tramite origini dati file](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)o la descrizione della funzione [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) .
