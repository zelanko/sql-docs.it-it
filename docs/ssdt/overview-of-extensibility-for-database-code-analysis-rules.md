---
title: Estendibilità delle regole di analisi del codice del database
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ef4ab84a123252dd35da85213110b8b4abb616ad
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251970"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>Panoramica dell'estendibilità delle regole di analisi del codice del database

Le edizioni di Visual Studio contenenti SQL Server Data Tools includono regole di analisi del codice per segnalare avvisi relativi alla progettazione, alla denominazione e alle prestazioni di Transact\-SQL nel codice del database. Per altre informazioni, vedere [Analisi del codice di database per migliorare la qualità del codice](https://msdn.microsoft.com/library/dd172133(v=vs.100).aspx).  
  
Se le regole di analisi del codice predefinite non coprono un problema di Transact\-SQL specifico che si vuole sia incluso, è possibile creare regole di analisi del codice del database personalizzate. Ad esempio, potrebbe essere necessario creare una regola personalizzata che eviti l'uso dell'istruzione WAITFOR DELAY, come illustrato in [Procedura dettagliata per la creazione di un assembly di regole personalizzate di analisi del codice statica per SQL Server](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md). Per creare le regole di analisi del codice del database personalizzate, è possibile usare le classi nello spazio dei nomi [CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx).  
  
Prima di creare le regole di analisi del codice personalizzate, è opportuno comprendere l'architettura di base tra i vari componenti delle regole di analisi del codice del database.  
  
## <a name="database-code-analysis-rules-components"></a>Componenti delle regole di analisi del codice del database  
La figura seguente illustra l'interazione tra i componenti delle regole di analisi del codice del database:  
  
![Componenti delle regole di analisi del codice del database](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "Componenti delle regole di analisi del codice del database")  
  
Quando si usa la funzionalità delle regole di analisi del codice del database, sia eseguendo direttamente l'analisi del codice statica (per altre informazioni, vedere [Procedura: Analizzare il codice Transact-SQL per trovare errori](https://msdn.microsoft.com/library/dd172119(v=vs.100).aspx)) che eseguendo una compilazione, tutte le regole vengono caricate e usate in base a come sono state configurate nel progetto. Per altre informazioni, vedere [Procedura: Abilitare e disabilitare regole specifiche relative all'analisi statica del codice del database](https://msdn.microsoft.com/library/dd172131(v=vs.100).aspx). Gestione estensioni caricherà inoltre qualsiasi assembly di regole personalizzate creato e registrato. Per altre informazioni, vedere [Procedura: Installare e gestire le estensioni delle funzionalità](../ssdt/how-to-install-and-manage-feature-extensions.md).  
  
Una classe di regola di analisi del codice personalizzata eredita da [SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx). La classe di regole personalizzate può accedere a diversi oggetti utili tramite il relativo contesto di esecuzione della regola, incluse le seguenti:  
  
-   Metadati relativi alla regola stessa.  
  
-   Oggetto Dac.Model.TSqlModel che rappresenta lo schema del database, inclusi tutti gli elementi del modello, le relazioni tra gli elementi e tutte le proprietà degli elementi.  
  
-   Per le regole che esaminano elementi specifici, viene incluso nel contesto l'oggetto Dac.Model.TSqlObject che rappresenta l'elemento dello schema nel modello.  
  
-   Molti oggetti dello schema contengono anche una rappresentazione di [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) a cui è possibile accedere tramite questo contesto. Si tratta di una rappresentazione basata sulla classe AST di un elemento che può essere utile per individuare potenziali problemi di sintassi, quali la presenza di [SelectStarExpression](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx).  
  
La regola crea un oggetto Dac.CodeAnalysis.SqlRuleProblem per rappresentare tutti i problemi rilevati. Quando viene creato questo oggetto, l'oggetto Dac.Model.TSqlObject appropriato ed eventualmente un elemento della rappresentazione di [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) vengono passati al costruttore e usati per determinare la posizione del problema nei file del codice sorgente. Al termine dell'analisi, tutti questi problemi vengono passati alla gestione errori e visualizzati nell'elenco errori.  
  
## <a name="see-also"></a>Vedere anche  
[Estensione delle funzionalità del database](../ssdt/extending-the-database-features.md)  
  
