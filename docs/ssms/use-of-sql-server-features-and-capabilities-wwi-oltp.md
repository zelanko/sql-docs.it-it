---
description: Strumenti esterni - Argomenti
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
ms.openlocfilehash: 4cf19970c7c742701248c362806bc823d38cf8a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88314957"
---
# <a name="arguments-for-external-tools"></a>Strumenti esterni - Argomenti
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 Gli argomenti sono variabili per le quali l'ambiente Visual Studio specifica dei valori quando viene avviato uno strumento esterno dal menu **Strumenti**. Al menu **Strumenti** è possibile aggiungere strumenti esterni, come il Blocco note, usando la finestra di dialogo **Strumenti esterni**.  
  
Nella tabella seguente vengono elencati gli argomenti per gli strumenti esterni.  
  
|NOME|Argomento|Descrizione|  
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
  
