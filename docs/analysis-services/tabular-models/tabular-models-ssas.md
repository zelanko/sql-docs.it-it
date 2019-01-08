---
title: I modelli tabulari in Analysis Services | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae7dfd78e71c41ab5b826a27742923445117417d
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072038"
---
# <a name="tabular-models"></a>Modelli tabulari
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  I modelli tabulari in Analysis Services sono i database in esecuzione in memoria o in modalità DirectQuery, la connessione ai dati direttamente dai dati relazionali di back-end di origini. Utilizzando il processore di query multithreading e algoritmi di compressione d'avanguardia, il motore di analitica Vertipaq di Analysis Services offre accesso rapido ai dati e agli oggetti modello tabulare da applicazioni client quali Excel e Power BI di creazione report.  
  
 Anche se i modelli in memoria sono l'impostazione predefinita, DirectQuery è una modalità di query alternativa usata per i modelli che sono troppo grandi per rientrare nella memoria o quando volatilità dei dati preclude una strategia di elaborazione ragionevole. DirectQuery raggiunge la parità con i modelli in memoria grazie al supporto per un'ampia gamma di origini dati, consentendo di gestire le tabelle calcolate e colonne in un modello DirectQuery, la sicurezza a livello di riga tramite espressioni DAX che raggiungono il database back-end ed eseguire query ottimizzazioni comportano una velocità effettiva.
  
 I modelli tabulari vengono creati in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando il modello di progetto di modello tabulare. Il modello di progetto fornisce un'area di progettazione per la creazione di oggetti modello semantico, ad esempio tabelle, partizioni, relazioni, gerarchie, le misure e indicatori KPI. 
  
 Modelli tabulari possono essere distribuiti a Azure Analysis Services o un'istanza di SQL Server Analysis Services configurata per la modalità server tabulare. I modelli tabulari distribuiti possono essere gestiti in SQL Server Management Studio. 

Si applica qui inclusa la documentazione di modellazione tabulare, nella maggior parte dei casi, sia SQL Server Analysis Services e Azure Analysis Services. Gli articoli specifici di Azure Analysis Services vengono pubblicati e altri documenti di Azure. Per altre informazioni, vedere [documentazione di Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).
  
