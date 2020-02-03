---
title: Creare un report tabella semplice (esercitazione su SSRS) | Microsoft Docs
ms.date: 04/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af41da75d553794019f1d01c8b8f5bb6aba80622
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65103310"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>Creare un report tabella semplice (esercitazione su SSRS)

In questa esercitazione si userà lo strumento *Progettazione report* in Visual Studio/SQL Server Data Tools (SSDT). Verrà creato un report impaginato SQL Server Reporting Services (SSRS), contenente una tabella di query creata dai dati del database AdventureWorks2016.

Nel corso dell'esercitazione verranno illustrate le procedure per:
  
- Creare un progetto report
- Configurare una connessione dati
- Definire una query
- Aggiungere un'area dati tabella
- Formattare il report
- Raggruppare i campi e ottenere i totali
- Visualizzare l'anteprima del report
- Pubblicare facoltativamente il report

## <a name="requirements"></a>Requisiti

Per completare l'esercitazione è necessario che nel sistema siano installati i componenti seguenti:

- [!INCLUDE[msconame-md](../includes/msconame-md.md)] Motore di database di SQL Server.  
- SQL Server 2016 Reporting Services (SSRS) o versioni successive.
- Database AdventureWorks2016.  Per altre informazioni, vedere [AdventureWorks Sample Databases](https://github.com/Microsoft/sql-server-samples/releases) (Database di esempio AdventureWorks).
- [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) per Visual Studio con l'estensione Reporting Services installata per consentire l'accesso a *Progettazione report*.
  
È anche necessario avere autorizzazioni di sola lettura per recuperare i dati dal database AdventureWorks2016.

**Tempo previsto per il completamento dell'esercitazione:** 30 minuti.

## <a name="next-steps"></a>Passaggi successivi

[Lezione 1: Creazione di un progetto server report &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)

[Lezione 2: Specifica delle informazioni di connessione &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)

[Lezione 3: Definizione di un set di dati per il report tabella &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)

[Lezione 4: Aggiunta di una tabella al report &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)

[Lezione 5: Formattazione di un report &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)

[Lezione 6: Aggiunta di gruppi e totali &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)

## <a name="see-also"></a>Vedere anche

[Esercitazioni su Reporting Services](reporting-services-tutorials-ssrs.md) Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
