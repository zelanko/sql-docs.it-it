---
title: Impostazione query di origine (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6da28ac9897681d963325fcaf7712f5ed4d3d88b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965517"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Impostazione query di origine (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **specificare una query di origine** per digitare l'istruzione SQL che genererà i dati da copiare dall'origine dati alla destinazione.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni di avvio della procedura guidata, nonché sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Istruzione SQL**  
 Consente di immettere un'istruzione di query per il recupero delle righe di dati selezionate dal database di origine. Ad esempio, l'istruzione di query seguente recupera i valori di **SalesPersonID**, **SalesQuota**e **SalesYTD** dal database AdventureWorks per i venditori la cui percentuale di Commissione è superiore al 1,5%.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **Analizzare**  
 Controlla la sintassi dell'istruzione SQL nella casella di testo **Istruzione SQL**.  
  
> [!NOTE]  
>  Se il tempo necessario per il controllo della sintassi dell'istruzione supera il valore di timeout di 30 secondi, l'analisi si arresta e viene generato un errore. Non sarà possibile andare oltre questa pagina della procedura guidata fino a quando l'analisi non avrà esito positivo. Una soluzione possibile consiste nel creare una vista di database basata sulla query ed eseguire la query sulla vista dalla procedura guidata, anziché immettere direttamente il testo della query.  
  
 **Sfoglia**  
 Consente di selezionare un file contenente un'istruzione SQL tramite la finestra di dialogo **Apri** . La selezione di un file copia il testo dal file nella casella di testo **istruzione query** .  
  
  
