---
title: Strumenti esterni - Argomenti
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 23c2680b2043ff35e882e801a684f8aeb9503b21
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010809"
---
# <a name="arguments-for-external-tools"></a>Strumenti esterni - Argomenti
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Gli argomenti sono variabili per le quali l'ambiente Visual Studio specifica dei valori quando viene avviato uno strumento esterno dal menu **Strumenti**. Al menu **Strumenti** è possibile aggiungere strumenti esterni, come il Blocco note, usando la finestra di dialogo **Strumenti esterni**.  
  
Nella tabella seguente vengono elencati gli argomenti per gli strumenti esterni.  
  
|Nome|Argomento|Descrizione|  
|--------|------------|---------------|  
|**Percorso elemento**|$(ItemPath)|Il nome file completo dell'origine corrente (definito come unità + percorso + nome file); vuoto se è attiva una finestra non di origine.|  
|**Directory elemento**|$(ItemDir)|La directory dell'origine corrente (definita come unità + percorso); vuoto se è attiva una finestra non di origine.|  
|**Nome file elemento**|$(ItemFilename)|Il nome file dell'origine corrente (definito come nome file); vuoto se è attiva una finestra non di origine.|  
|**Estensione elemento**|$(ItemExt)|L'estensione del nome file dell'origine corrente.|  
|**Riga corrente***|$(CurLine)|La posizione di riga corrente del cursore nell'editor.|  
|**Colonna corrente***|$(CurCol)|La posizione di colonna corrente del cursore nell'editor.|  
|**Testo corrente***|$(CurText)|Il testo corrente (la parola sotto la posizione corrente del cursore o selezione di una riga singola, se presente).|  
|**Percorso di destinazione**|$(TargetPath)|Il nome file completo della destinazione (definito come unità + percorso + nome file).|  
|**Directory di destinazione**|$(TargetDir)|La directory della destinazione.|  
|**Nome destinazione**|$(TargetName)|Il nome file della destinazione.|  
|**Estensione di destinazione**|$(TargetExt)|L'estensione del nome file della destinazione.|  
|**Directory progetto**|$(ProjDir)|La directory del progetto corrente (definita come unità + percorso).|  
|**Nome file progetto**|$(ProjFileName)|Il nome file del progetto corrente (definito come unità + percorso + nome file).|  
|**Directory soluzione**|$(SolutionDir)|La directory della soluzione corrente (definita come unità + percorso).|  
|**Nome file soluzione**|$(SolutionFileName)|Il nome file della soluzione corrente (definito come unità + percorso + nome file).|  
  
*La riga, la colonna o il testo corrente dipendono dalla posizione del cursore nell'editor di testo, come indicato nella barra di stato.  
  
## <a name="see-also"></a>Vedere anche  
[Finestra di dialogo Strumenti esterni](../ssms/external-tools-dialog-box.md)  
[Elementi generali dell'interfaccia utente](../ssms/general-user-interface-elements.md)  
  
