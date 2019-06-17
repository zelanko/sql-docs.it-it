---
title: Istruzione CREATE INDEX | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93ddc3881796aee3194ec5268afc68ecbab1a487
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232997"
---
# <a name="create-index-statement"></a>Istruzione CREATE INDEX
La sintassi dell'istruzione CREATE INDEX è:  
  
 Crea indice [UNIQUE] *-nome dell'indice* via *nome-tabella* (*identificatore di colonna* [Centro sicurezza di AZURE] [DESC] [, *colonna identificatore* [ASC][DESC]...]) CON \< *elenco di opzioni di indice*>  
  
 in cui \< *elenco di opzioni di indice*> può essere: PRIMARIO &AMP;#124; NULL NON CONSENTIRE &AMP;#124; IGNORA NULL  
  
 Solo il driver Microsoft Access usa le opzioni di indice impedisce NULL e Ignora NULL. Il file dBASE e i driver Paradox accetta la sintassi, ma ignoreranno la presenza di entrambe le opzioni.  
  
 Quando viene usato il driver Paradox, l'istruzione CREATE INDEX crea i file di chiave primari Paradox e file secondari.  
  
 Questa istruzione non è supportata dai driver Microsoft Excel o di testo.
