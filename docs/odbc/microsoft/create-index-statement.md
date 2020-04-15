---
title: Istruzione CREATE INDEX Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280971"
---
# <a name="create-index-statement"></a>Istruzione CREATE INDEX
La sintassi dell'istruzione CREATE INDEX è la seguente:  
  
 CREATE [UNIQUE] INDEX *index-name* ON *table-name* (*column-identifier* [ASC][DESC][, *column-identifier* [ASC][DESC]...]) Elenco \< *di opzioni* con indice>  
  
 dove \< *l'elenco* di opzioni indice può essere>: PRIMARY &#124; DISALLOW NULL &#124; IGNORE NULL  
  
 Solo il driver di Microsoft Access utilizza le opzioni di indice DISALLOW NULL e IGNORE NULL. I driver dBASE e Paradox accettano la sintassi, ma ignorano la presenza di entrambe le opzioni.  
  
 Quando viene utilizzato il driver Paradox, l'istruzione CREATE INDEX crea i file di chiave primaria di Paradox e i file secondari.  
  
 Questa istruzione non è supportata dai driver di Microsoft Excel o di testo.
