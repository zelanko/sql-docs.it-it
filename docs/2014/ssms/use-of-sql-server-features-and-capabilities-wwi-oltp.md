---
title: Argomenti per gli strumenti esterni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2365ec137329675e2cd88e7f5bf7e1781aa3308f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280485"
---
# <a name="arguments-for-external-tools"></a>Strumenti esterni - Argomenti
  Gli argomenti sono variabili per le quali l'ambiente Visual Studio specifica dei valori quando viene avviato uno strumento esterno dal menu **Strumenti**. Al menu **Strumenti** è possibile aggiungere strumenti esterni, come il Blocco note, usando la finestra di dialogo **Strumenti esterni**.  
  
 Nella tabella seguente vengono elencati gli argomenti per gli strumenti esterni.  
  
|nome|Argomento|Descrizione|  
|----------|--------------|-----------------|  
|**Percorso elemento**|$(ItemPath)|Il nome file completo dell'origine corrente (definito come unità + percorso + nome file); vuoto se è attiva una finestra non di origine.|  
|**Directory elemento**|$(ItemDir)|La directory dell'origine corrente (definita come unità + percorso); vuoto se è attiva una finestra non di origine.|  
|**Nome file elemento**|$(ItemFilename)|Il nome file dell'origine corrente (definito come nome file); vuoto se è attiva una finestra non di origine.|  
|**Estensione elemento**|$(ItemExt)|L'estensione del nome file dell'origine corrente.|  
|**Riga corrente** <sup>1</sup>|$(CurLine)|La posizione di riga corrente del cursore nell'editor.|  
|**Colonna corrente**1|$(CurCol)|La posizione di colonna corrente del cursore nell'editor.|  
|**Testo corrente**1|$(CurText)|Il testo corrente (la parola sotto la posizione corrente del cursore o selezione di una riga singola, se presente).|  
|**Percorso di destinazione**|$(TargetPath)|Il nome file completo della destinazione (definito come unità + percorso + nome file).|  
|**Directory di destinazione**|$(TargetDir)|La directory della destinazione.|  
|**Nome destinazione**|$(TargetName)|Il nome file della destinazione.|  
|**Estensione di destinazione**|$(TargetExt)|L'estensione del nome file della destinazione.|  
|**Directory progetto**|$(ProjDir)|La directory del progetto corrente (definita come unità + percorso).|  
|**Nome file progetto**|$(ProjFileName)|Il nome file del progetto corrente (definito come unità + percorso + nome file).|  
|**Directory soluzione**|$(SolutionDir)|La directory della soluzione corrente (definita come unità + percorso).|  
|**Nome file soluzione**|$(SolutionFileName)|Il nome file della soluzione corrente (definito come unità + percorso + nome file).|  
  
 <sup>1</sup> la riga corrente, la colonna corrente o testo corrente è basato sulla posizione del cursore nell'editor di testo, come mostrato nella barra di stato.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Strumenti esterni](external-tools-dialog-box.md)   
 [Elementi generali dell'interfaccia utente](general-user-interface-elements.md)  
  
  
