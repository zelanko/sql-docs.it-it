---
title: Gli indici full-text su colonne calcolate non salvate non sono consentiti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: de153d45e2f652bfea6e9dce68428af84be68b6c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012341"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>Gli indici full-text su colonne calcolate non persistenti non sono consentiti
  Non è possibile creare indici full-text in colonne calcolate non deterministiche e imprecise. Non è possibile utilizzare tali colonne come colonne tipo o come colonne chiave full-text.  
  
## <a name="description"></a>Descrizione  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] è possibile creare un indice full-text utilizzando una colonna calcolata non deterministica e imprecisa come colonna tipo o come colonna chiave full-text. Questa funzionalità non è supportata. Quando si esegue l'aggiornamento, gli indici full-text precedenti, incompatibili e non supportati vengono disabilitati.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per abilitare questi indici full-text, modificare le definizioni di colonna in modo che le colonne siano deterministiche e precise.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
