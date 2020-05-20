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
author: rothja
ms.author: jroth
ms.openlocfilehash: 02f4be413ddcfc9215cdbf12142b883ade644f41
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761117"
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
