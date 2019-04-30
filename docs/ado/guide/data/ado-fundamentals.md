---
title: Nozioni fondamentali su ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 448eda8c3c77f410bedd88d1193f2302c926ee95
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062927"
---
# <a name="ado-fundamentals"></a>Nozioni fondamentali su ADO
ADO offre agli sviluppatori un modello a oggetti potenti e logica per l'accesso a livello di codice, la modifica e aggiornamento dei dati da una vasta gamma di origini dati tramite le interfacce OLE DB di sistema. L'uso più comune di ADO è eseguire la query una o più tabelle in un database relazionale, recuperare e visualizzare i risultati in un'applicazione e forse consentire agli utenti di creare e salvare le modifiche ai dati. Altre attività includono quanto segue:  
  
-   Esecuzione di query su un database tramite SQL e la visualizzazione dei risultati.  
  
-   L'accesso alle informazioni in un archivio file su Internet.  
  
-   Modifica di messaggi e le cartelle in un sistema di posta elettronica.  
  
-   Salvataggio dei dati da un database in un file XML.  
  
-   L'esecuzione di comandi descritti con XML e il recupero di un flusso XML.  
  
-   Salvataggio dei dati in un flusso binario o XML.  
  
-   Che consente all'utente di esaminare e modificare i dati nelle tabelle di database.  
  
-   Creando e riutilizzando i comandi di database con parametri.  
  
-   Esecuzione di stored procedure.  
  
-   La creazione dinamica di una struttura flessibile, che viene denominata una **Recordset**, per contenere, visualizzare e modificare i dati.  
  
-   Esecuzione di operazioni di database transazionale.  
  
-   Filtro e ordinamento copie locali delle informazioni del database in base ai criteri di runtime.  
  
-   Creazione e modifica delle risultati gerarchici dal database.  
  
-   Associazione dei campi di database per i componenti che supportano i dati.  
  
-   Creazione di remoti disconnessi **recordset**.  
  
 ADO espone un'ampia gamma di opzioni e impostazioni per fornire una notevole flessibilità. Pertanto, è importante adottare un approccio metodico per imparare a utilizzare ADO in un'applicazione, suddividendo i singoli obiettivi in gestibili.  
  
 Quattro operazioni principali coinvolti nella maggior parte delle applicazioni che utilizzano ADO: recupero di dati, analisi dei dati, la modifica dei dati e l'aggiornamento dei dati. Queste operazioni vengono esaminate in dettaglio più avanti in questa sezione.  
  
 Tuttavia, prima di spiegare questi dettagli, verrà presentata una panoramica del modello a oggetti ADO e una semplice applicazione di ADO, che viene scritto in Microsoft® Visual Basic® ed esegue ognuna delle quattro operazioni ADO primarie:  
  
-   [Oggetti e raccolte di ADO](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: Un'applicazione semplice ADO](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [Provider OLE DB](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [errori](../../../ado/guide/data/errors-ado.md)
