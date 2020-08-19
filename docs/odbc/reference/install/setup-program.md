---
description: Programma di installazione
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cd4858214ff084a037002abd3bd34035160496b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421325"
---
# <a name="setup-program"></a>Programma di installazione
> **Nota:** A partire da Windows XP e Windows Server 2003, **ODBC è incluso nel sistema operativo Windows**. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 L'utente esegue il programma di installazione di per avviare il processo di installazione. Il programma di installazione viene scritto dallo sviluppatore dell'applicazione o del driver. Oltre all'installazione dei componenti ODBC, è possibile installare altri software. Gli sviluppatori di applicazioni possono ad esempio utilizzare lo stesso programma di installazione per installare i componenti ODBC e per installare le applicazioni.  
  
 Gli sviluppatori possono scrivere il programma di installazione da zero, usando le utilità di installazione di Microsoft® Windows® SDK o il software di installazione di altri fornitori. Questo consente agli sviluppatori di controllare completamente l'aspetto del programma di installazione. È possibile scrivere il programma di installazione per installare software aggiuntivo, ad esempio un'applicazione ODBC. Per ulteriori informazioni sulle utilità di installazione di Windows SDK, vedere la documentazione di Windows SDK.  
  
 La quantità di installazione effettivamente eseguita dal programma di installazione dipende dalle funzioni che chiama nella DLL di installazione. La DLL del programma di installazione contiene funzioni per l'installazione di singoli componenti ODBC. Il programma di installazione chiama semplicemente **SQLInstallDriverManager**, **SQLInstallDriverEx**o **SQLInstallTranslatorEx** nella dll del programma di installazione per recuperare il percorso della directory in cui deve essere installato il componente e per aggiungere informazioni sul componente al registro di sistema. Queste funzioni non copiano effettivamente i file; il programma di installazione esegue questa operazione utilizzando le informazioni contenute negli argomenti di queste funzioni.  
  
 La DLL del programma di installazione contiene anche funzioni per la rimozione dei componenti ODBC. Il programma di installazione chiama **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator** nella dll del programma di installazione per decrementare il numero di utilizzo di un componente nel registro di sistema e, se il nuovo conteggio di utilizzo del componente scende a 0, rimuovere tutte le informazioni sul componente dal registro di sistema. Queste funzioni non rimuovono effettivamente i file per il componente; il programma di installazione esegue questa operazione se il nuovo conteggio di utilizzo è pari a 0.
