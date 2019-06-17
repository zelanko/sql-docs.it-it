---
title: Programma di installazione | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f64eda5ad640e50afd25db111de74141e41e652d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280783"
---
# <a name="setup-program"></a>Programma di installazione
> **NOTA:** A partire da Windows XP e Windows Server 2003, **ODBC è incluso nel sistema operativo Windows**. Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 L'utente esegue il programma di installazione per avviare il processo di installazione. Il programma di installazione viene scritto dallo sviluppatore dell'applicazione o driver. Oltre a installare i componenti ODBC, può installare altro software. Ad esempio, gli sviluppatori di applicazioni usino lo stesso programma di installazione per installare i componenti ODBC sia per installare le proprie applicazioni.  
  
 Gli sviluppatori possono scrivere il programma di installazione da zero, usando l'utilità di installazione di Microsoft® Windows® SDK o il software di installazione di altri fornitori. In questo modo gli sviluppatori che controllo completo sull'aspetto del programma di installazione. Il programma di installazione può essere scritti per installare software aggiuntivo, ad esempio un'applicazione ODBC. Per ulteriori informazioni sull'utilità di installazione Windows SDK, vedere la documentazione di Windows SDK.  
  
 Quanta parte dell'installazione viene effettivamente eseguita dal programma di installazione dipende da quali funzioni chiamate nel programma di installazione DLL. Il programma di installazione DLL contiene funzioni per installare i singoli componenti ODBC. Il programma di installazione consente di chiamare semplicemente **SQLInstallDriverManager**, **SQLInstallDriverEx**, o **SQLInstallTranslatorEx** nella DLL per recuperare il percorso del programma di installazione di Directory in cui il componente da installare e aggiungere informazioni sul componente al Registro di sistema. Queste funzioni non copiano effettivamente i file; il programma di installazione avviene mediante le informazioni negli argomenti di queste funzioni.  
  
 Il programma di installazione DLL contiene anche le funzioni per rimuovere i componenti ODBC. Il programma di installazione chiami **SQLRemoveDriverManager**, **SQLRemoveDriver**, o **SQLRemoveTranslator** nel programma di installazione di conteggio DLL per diminuire l'utilizzo di un componente di Registro di sistema e, se il nuovo conteggio di utilizzo del componente scende a 0, rimuovere tutte le informazioni sul componente dal Registro di sistema. Queste funzioni non rimuovono i file per il componente; in realtà il programma di installazione avviene se il nuovo conteggio di utilizzo scende a 0.
