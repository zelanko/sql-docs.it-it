---
description: Uso delle origini dati
title: Uso di origini dati | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 162f1c2bf8d75757ac2c29d60f675ac07ba8b00d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428833"
---
# <a name="using-data-sources"></a>Uso delle origini dati
Le origini dati vengono in genere create dall'utente finale o da un tecnico con un programma denominato *amministratore ODBC*. L'amministratore ODBC chiede all'utente di usare e quindi chiama tale driver. Il driver Visualizza una finestra di dialogo che richiede le informazioni necessarie per la connessione all'origine dati. Dopo che l'utente immette le informazioni, il driver lo archivia nel sistema.  
  
 Successivamente, l'applicazione chiama Gestione driver e passa il nome di un'origine dati del computer o il percorso di un file contenente un'origine dati file. Quando viene passato il nome di un'origine dati del computer, gestione driver esegue una ricerca nel sistema per trovare il driver usato dall'origine dati. Quindi carica il driver e lo passa al nome dell'origine dati. Il driver utilizza il nome dell'origine dati per trovare le informazioni necessarie per la connessione all'origine dati. Infine, si connette all'origine dati, in genere richiedendo all'utente un ID utente e una password, che in genere non vengono archiviati.  
  
 Quando viene passata un'origine dati file, gestione driver apre il file e carica il driver specificato. Se il file contiene anche una stringa di connessione, la passa al driver. Utilizzando le informazioni contenute nella stringa di connessione, il driver si connette all'origine dati. Se non è stata passata alcuna stringa di connessione, il driver richiede in genere all'utente le informazioni necessarie.
