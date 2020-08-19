---
description: Converti tipi senza eseguire i controlli di conversione (Importazione/Esportazione guidata SQL Server)
title: Converti tipi senza eseguire i controlli di conversione (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.nomappingfile.f1
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5d7c53d4117d7634b6651069260c289657f82315
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88391467"
---
# <a name="convert-types-without-conversion-checking-sql-server-import-and-export-wizard"></a>Converti tipi senza eseguire i controlli di conversione (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Dopo aver selezionato le tabelle e le viste per copiare o rivedere la query fornita, l’Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe mostrare **Converti tipi senza eseguire i controlli di conversione**. La procedura guidata visualizza questa pagina quando non è in grado di individuare uno o più file di conversione dei tipi di dati e di mapping necessari per mappare i tipi di dati tra origine e destinazione. La pagina contiene informazioni che semplificano l’individuazione di cosa manca.
  
 Fare clic su **Avanti** per continuare senza sapere se le conversioni dei tipi di dati avranno esito positivo. In alternativa, fare clic su **Indietro** per modificare le selezioni oppure fare clic su **Annulla** per uscire dalla procedura guidata.

## <a name="screen-shot-of-the-convert-types-page"></a>Screenshot della pagina Converti tipi  
  
La schermata riportata di seguito mostra un esempio della pagina **Converti tipi senza eseguire i controlli di conversione** della procedura guidata.

![Conversione dei tipi](../../integration-services/import-export-data/media/convert-types.png)

Il problema è che la procedura guidata non è in grado di trovare un file di mapping che esegue il mapping dei tipi di dati per la destinazione selezionata.

Le informazioni contenute in questa pagina non includono il nome del file di mapping mancante. Poiché la procedura guidata non sa se esiste un file per il provider di dati specificato, non può indicare il nome del file mancante.

## <a name="whats-next"></a>Passaggi successivi  
 Dopo aver fatto clic su **Avanti** per continuare senza sapere se le conversioni dei tipi di dati avranno esito positivo, la pagina successiva visualizzata è **Salvare ed eseguire il pacchetto**. In questa pagina specificare se eseguire immediatamente l'operazione di copia. A seconda della configurazione, è anche possibile salvare il pacchetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creato dalla procedura guidata per personalizzarlo e usarlo di nuovo in seguito. Per altre informazioni, vedere [Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Vedi anche
[Mapping dei tipi di dati nell'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
