---
title: Utilizzo delle origini dati . Documenti Microsoft
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
ms.openlocfilehash: df9b09e4c5519e0fff44902bd83b8e3d92a67ca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286552"
---
# <a name="using-data-sources"></a>Uso delle origini dati
Le origini dati vengono in genere create dall'utente finale o da un tecnico con un programma denominato *Amministratore ODBC*. L'Amministratore ODBC richiede all'utente per il driver da utilizzare e quindi chiama tale driver. Il driver visualizza una finestra di dialogo che richiede le informazioni necessarie per connettersi all'origine dati. Dopo che l'utente immette le informazioni, il driver le archivia nel sistema.  
  
 Successivamente, l'applicazione chiama Gestione Driver e le passa il nome di un'origine dati macchina o il percorso di un file contenente un'origine dati file. Quando viene passato un nome di origine dati macchina, Gestione Driver cerca il sistema per trovare il driver utilizzato dall'origine dati. Carica quindi il driver e vi passa il nome dell'origine dati. Il driver utilizza il nome dell'origine dati per trovare le informazioni necessarie per connettersi all'origine dati. Infine, si connette all'origine dati, in genere richiedendo all'utente un ID utente e una password, che in genere non vengono archiviati.  
  
 Quando viene passata un'origine dati file, Gestione Driver apre il file e carica il driver specificato. Se il file contiene anche una stringa di connessione, passa questo al driver. Utilizzando le informazioni nella stringa di connessione, il driver si connette all'origine dati. Se non è stata passata alcuna stringa di connessione, il driver richiede in genere all'utente le informazioni necessarie.
