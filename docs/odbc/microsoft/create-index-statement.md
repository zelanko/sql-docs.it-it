---
title: CREATE INDEX-istruzione | Microsoft Docs
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
ms.openlocfilehash: ad15ad436b0f34f00acbd75e371e998183f22d2f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081913"
---
# <a name="create-index-statement"></a>Istruzione CREATE INDEX
La sintassi dell'istruzione CREATE INDEX è la seguente:  
  
 CREATE [UNIQUE] index *index-name* sul *nome di tabella* (*column-identifier* [ASC] [Desc] [, *column-identifier* [ASC] [Desc]...]) \< *Elenco di opzioni con indice*>  
  
 dove \<> *elenco di opzioni di indice* può essere: Primary &#124; non consentire null &#124; ignore null  
  
 Solo il driver Microsoft Access utilizza le opzioni non consentire valori NULL e ignora Indice NULL. I driver dBASE e Paradox accettano la sintassi, ma ignorano la presenza di una delle due opzioni.  
  
 Quando si utilizza il driver Paradox, l'istruzione CREATE INDEX crea file di chiave primaria e file secondari di Paradox.  
  
 Questa istruzione non è supportata dai driver di Microsoft Excel o di testo.
