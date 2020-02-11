---
title: Caratteristiche del cursore e del blocco | Microsoft Docs
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
ms.openlocfilehash: c4d6f86539e1abc7ee74087b130e0186322346e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925670"
---
# <a name="cursor-and-lock-characteristics"></a>Caratteristiche dei cursori e dei blocchi
Sebbene le caratteristiche di un cursore dipendano dalle funzionalità del provider, i vantaggi e gli svantaggi seguenti si applicano in genere ai vari tipi di cursori e blocchi.  
  
|Cursore o tipo di blocco|Vantaggi|Svantaggi|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisiti di risorse insufficienti|-Impossibile scorrere all'indietro<br />-Nessuna concorrenza dei dati|  
|**adOpenStatic**|-Scorrevole|-Nessuna concorrenza dei dati|  
|**adOpenKeyset**|-Parte della concorrenza dei dati<br />-Scorrevole|-Requisiti di risorse maggiori<br />-Non disponibile in uno scenario disconnesso|  
|**adOpenDynamic**|-Concorrenza elevata dei dati<br />-Scorrevole|-Requisiti massimi per le risorse<br />-Non disponibile in uno scenario disconnesso|  
|**adLockReadOnly**|-Requisiti di risorse insufficienti<br />-Scalabilità elevata|-Dati non aggiornabili tramite cursore|  
|**adLockBatchOptimistic**|-Aggiornamenti batch<br />-Consente scenari disconnessi<br />-Altri utenti in grado di accedere ai dati|-I dati possono essere modificati contemporaneamente da più utenti|  
|**adLockPessimistic**|-I dati non possono essere modificati da altri utenti durante il blocco|-Impedisce ad altri utenti di accedere ai dati durante il blocco|  
|**adLockOptimistic**|-Altri utenti in grado di accedere ai dati|-I dati possono essere modificati contemporaneamente da più utenti|
