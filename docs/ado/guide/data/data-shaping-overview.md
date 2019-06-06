---
title: Panoramica del Data Shaping | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d693ccbeb06860cd4633a933e80b9ccbe6526a8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702229"
---
# <a name="data-shaping-overview"></a>Panoramica del data shaping
*Il data shaping* la creazione di relazioni gerarchiche tra due o più entità logiche in una query. La gerarchia può essere visualizzata in una relazione padre-figlio tra un record di uno [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e uno o più record (noto anche come un capitolo) di un'altra **Recordset**. In una relazione padre-figlio, l'elemento padre **Recordset** contiene l'elemento figlio **Recordset**. Un esempio di tale relazione gerarchica è customers e orders. Per ogni cliente in un database, possono essere presenti zero o più ordini. La relazione gerarchica può essere ricorsivo, vale a dire che i record nipote possono essere annidati in un record figlio. In teoria, un record gerarchico può essere annidato a qualsiasi profondità. In pratica, ADO limita la ricorsione per un massimo di 512 **Recordset**s.  
  
 In generale, colonne di una data shaping **Recordset** può contenere i dati da un provider di dati, ad esempio Microsoft® SQL Server, i riferimenti a un'altra **Recordset**, valori derivati da un calcolo su una singola riga di una  **Recordset**, o valori derivati da un'operazione su una colonna di un'intera **Recordset**. Una colonna può inoltre essere appena creato e vuota.  
  
 Quando si recupera il valore di una colonna che contiene un riferimento a un'altra **Recordset**, ADO restituisce automaticamente l'effettivo **Recordset** rappresentata dal riferimento. Il riferimento a un **Recordset** è effettivamente un riferimento a un sottoinsieme dell'oggetto figlio, denominato un *capitolo*. Un singolo elemento padre può fare riferimento a più di un elemento figlio **Recordset**.  
  
 Supporto di ADO per il data shaping dei dati consente di eseguire query di un'origine dati e restituire un **Recordset** in cui un record (padre) rappresenta un elemento (figlio) **Recordset**. Nello scenario di ordine cliente, è possibile usare i dati di data shaping per recuperare le informazioni dei clienti, nonché gli ordini eseguiti da ogni cliente in una singola query. I risultanti **Recordset** noto anche come la forma **Recordset**.  
  
 Inoltre, data shaping in ADO consente di creare un nuovo **Recordset** oggetti senza un'origine dati sottostante utilizzando il **NEW** parola chiave per descrivere i campi dell'elemento padre e figlio  **Recordset**. Il nuovo **Recordset** oggetto può essere popolato con i dati e memorizzato in modo permanente. Gli sviluppatori possono anche eseguire varie calcoli o aggregazioni (ad esempio, **somma**, **AVG**, e **MAX**) in campi secondari. Il data shaping anche possibile creare un elemento padre **Recordset** da un elemento figlio **Recordset** raggruppando i record nell'elemento figlio e l'inserimento di una riga per ogni gruppo di nell'elemento figlio del padre.  
  
 Il linguaggio SQL standard consente di recuperare i dati usando **JOIN** sintassi, ma ciò può risultare a inefficiente e difficile da gestire perché dati ridondanti padre viene ripetuti in ogni record restituiti per una relazione padre-figlio specificata. Il data shaping possibile correlare un record singolo elemento padre del padre **Recordset** a più record figlio nell'elemento figlio **Recordset**, evitando la ridondanza di un **JOIN**. La maggior parte degli utenti ritengono padre-figlio più **Recordset** modello di programmazione più naturale e più facile lavorare con più il singolo **Recordset JOIN** modello.
