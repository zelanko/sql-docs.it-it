---
description: Creazione di programmi SMO
title: Creazione di programmi SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b55530e34a77878c551dc8ea4ff0fa2936325755
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490441"
---
# <a name="creating-smo-programs"></a>Creazione di programmi SMO
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  La programmazione generale degli oggetti [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) include le aree comuni condivise da tutti gli oggetti, ad esempio l'esecuzione di metodi, l'impostazione di proprietà e la manipolazione di raccolte.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Connessione a un'istanza di SQL Server](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|Il programma SMO più semplice che stabilisce una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Vengono illustrate l'autenticazione di Windows e l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e vengono forniti esempi di connessione a un'istanza locale e a un'istanza remota di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Disconnessione da un'istanza di SQL Server](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|Programma che illustra come eseguire la disconnessione dall'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Chiamata di metodi](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|In questa sezione viene descritto l'approccio generale alla chiamata dei metodi. Viene illustrato l'utilizzo dei parametri e la gestione delle tabelle di dati restituite in un oggetto <xref:System.Data.DataTable>. Include anche un esempio di come chiamare un costruttore di oggetto e come chiamare il metodo **Clone** .|  
|[Impostazione delle proprietà - SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|In questa sezione viene illustrato come impostare diversi tipi di proprietà, come impostare e ottenere le proprietà degli oggetti e, attraverso gli esempi forniti, come impostare le proprietà dell'oggetto al momento della creazione e come  scorrere tutte le proprietà di un oggetto.|  
|[Utilizzo delle raccolte](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|Vari programma che illustrano le tecniche utilizzate con le raccolte di oggetti. Viene spiegato come fare riferimento a un oggetto tramite le raccolte e, attraverso gli esempi forniti, come scorrere i membri di una raccolta.|  
|[Gestione degli eventi SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|In questa sezione viene descritto come impostare e gestire eventi in SMO e viene fornito un esempio su come impostare un gestore eventi e una sottoscrizione di eventi.|  
|[Gestione delle eccezioni SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|In questa sezione viene illustrato come intercettare le eccezioni in SMO attraverso esempi di intercettazioni e di visualizzazione di un'eccezione interna.|  
|[Utilizzo dei tipi di dati](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|In questa sezione viene illustrato come utilizzare i diversi tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], come costruire un oggetto datatype con la specifica nel costruttore di oggetti e viene fornito un esempio di creazione di un oggetto datatype tramite il costruttore predefinito.|  
|[Utilizzo di transazioni](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|In questa sezione viene illustrato come implementare l'elaborazione delle transazioni in un programma SMO e vengono forniti esempi di utilizzo delle transazioni in questo tipo di programmi.|  
|[Utilizzo della modalità di acquisizione](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|In questa sezione viene illustrato come registrare l'output del programma SMO. Nell'esempio il programma SMO viene registrato sotto forma di istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] inviate all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per un'esecuzione successiva.|  
  
  
