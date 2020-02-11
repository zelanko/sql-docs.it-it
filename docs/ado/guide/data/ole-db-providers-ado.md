---
title: Provider di OLE DB (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e86375639d875f5cfec21705af47c005afd901e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924752"
---
# <a name="ole-db-providers-ado"></a>Provider OLE DB (ADO)
OLE DB definisce un set di interfacce COM che consentono alle applicazioni di accedere in modo uniforme ai dati archiviati in origini dati diverse. Questo approccio consente a un'origine dati di condividere i dati attraverso le interfacce che supportano la quantità di funzionalità DBMS appropriate per l'origine dati. Per impostazione predefinita, l'architettura a prestazioni elevate di OLE DB si basa sull'utilizzo di un modello di servizi flessibile basato su componenti. Anziché avere un numero prescritto di livelli intermedi tra l'applicazione e i dati, OLE DB richiede solo il numero di componenti necessari per eseguire una determinata attività.  
  
 Si supponga, ad esempio, che un utente desideri eseguire una query. Esaminare gli scenari seguenti:  
  
-   I dati si trovano in un database relazionale per il quale esiste attualmente un driver ODBC ma non un provider di OLE DB nativo: l'applicazione utilizza ADO per comunicare con il provider OLE DB per ODBC, che quindi carica il driver ODBC appropriato. Il driver passa l'istruzione SQL al sistema DBMS, che recupera i dati.  
  
-   I dati si trovano in Microsoft SQL Server per cui è presente un provider di OLE DB nativo: l'applicazione usa ADO per comunicare direttamente con il provider di OLE DB per Microsoft SQL Server. Non è richiesto alcun intermediario.  
  
-   I dati si trovano in Microsoft Exchange Server, per il quale è disponibile un provider di OLE DB ma che non espone un motore per elaborare le query SQL: l'applicazione utilizza ADO per comunicare con il provider di OLE DB per Microsoft Exchange e chiama su un processore di query OLE DB componente per la gestione delle query.  
  
-   I dati si trovano nel file system Microsoft NTFS sotto forma di documenti: i dati sono accessibili tramite un provider di OLE DB nativo sul servizio di indicizzazione Microsoft, che indicizza il contenuto e le proprietà dei documenti nel file system per consentire contenuto efficiente Cerca.  
  
 In tutti gli esempi precedenti, l'applicazione può eseguire query sui dati. Le esigenze dell'utente sono soddisfatte da un numero minimo di componenti. In ogni caso, i componenti aggiuntivi vengono utilizzati solo se necessario e vengono richiamati solo i componenti richiesti. Questo caricamento su richiesta di componenti riutilizzabili e condivisibile contribuisce significativamente a prestazioni elevate quando si usa OLE DB.  
  
 I provider rientrano in due categorie, ovvero quelle che forniscono i dati e i servizi. Un provider di dati possiede i propri dati e li espone in forma tabulare all'applicazione. Un provider di servizi incapsula un servizio tramite la produzione e l'utilizzo di dati, aumentando le funzionalità nelle applicazioni ADO. Un provider di servizi può anche essere definito ulteriormente come un componente del servizio, che deve funzionare insieme ad altri provider di servizi o componenti.  
  
 ADO fornisce un'interfaccia coerente e di livello superiore ai vari provider di OLE DB.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Provider di dati](../../../ado/guide/data/data-providers.md)  
  
-   [Provider di servizi e componenti](../../../ado/guide/data/service-providers-and-components.md)
