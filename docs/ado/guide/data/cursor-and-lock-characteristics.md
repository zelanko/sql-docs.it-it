---
title: Cursore e le caratteristiche di blocco | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3a206a21cf7c6680a656c89c48b8f52d1069d78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702119"
---
# <a name="cursor-and-lock-characteristics"></a>Caratteristiche dei cursori e dei blocchi
Mentre le caratteristiche di un cursore dipendono dalle funzionalità del provider, i seguenti vantaggi e svantaggi in genere si applicano ai vari tipi di cursori e blocchi.  
  
|Tipo di cursore o di blocco|Vantaggi|Svantaggi|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisiti di risorse basso|-Non è possibile scorrere all'indietro<br />-Nessun concorrenza dei dati|  
|**adOpenStatic**|-Scorrevole|-Nessun concorrenza dei dati|  
|**adOpenKeyset**|-Alcuni concorrenza dei dati<br />-Scorrevole|-Più elevati requisiti di risorse<br />-Non disponibile in uno scenario disconnesso|  
|**adOpenDynamic**|-Concorrenza dei dati alto<br />-Scorrevole|-Requisiti di risorse massimo<br />-Non disponibile in uno scenario disconnesso|  
|**adLockReadOnly**|-Requisiti di risorse basso<br />-Altamente scalabili|-I dati non è aggiornabili tramite cursore|  
|**adLockBatchOptimistic**|-Gli aggiornamenti in batch<br />-Consente gli scenari disconnessi<br />-Altri utenti in grado di accedere ai dati|-Dati possono essere modificati contemporaneamente da più utenti|  
|**adLockPessimistic**|-Data non può essere modificato da altri utenti durante il blocco|-Impedisce ad altri utenti l'accesso ai dati durante il blocco|  
|**adLockOptimistic**|-Altri utenti in grado di accedere ai dati|-Dati possono essere modificati contemporaneamente da più utenti|
