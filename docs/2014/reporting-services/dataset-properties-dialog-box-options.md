---
title: Finestra di dialogo Proprietà set di dati, opzioni | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10130"
- sql12.rtp.rptdesigner.datasetproperties.options.f1
ms.assetid: 95299049-71ba-427f-b723-775cb696243f
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 502d3636998b6bdcebd8f3ac9044bd5df14bd66e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029862"
---
# <a name="dataset-properties-dialog-box-options"></a>Finestra di dialogo Proprietà set di dati, Opzioni
  Selezionare **le opzioni** nel **proprietà set di dati** finestra di dialogo per modificare le opzioni di dati, ad esempio le regole di confronto e i subtotali, per la query. Per altre informazioni, vedere [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="options"></a>Opzioni  
 **Confronto**  
 Consente di selezionare le impostazioni locali che determinano la sequenza di regole di confronto da utilizzare per l'ordinamento dei dati. Il valore**Default** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se non è possibile recuperare il valore, il valore predefinito viene ottenuto in base alle impostazioni locali del computer.  
  
 **Distinzione maiuscole/minuscole**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione tra maiuscole e minuscole. Questa opzione indica se per i dati viene applicata la distinzione tra maiuscole e minuscole. È possibile impostare l'opzione **Distinzione maiuscole/minuscole** su **True**, **False**o **Auto**. Il valore predefinito **Auto** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione tra maiuscole e minuscole, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione caratteri accentati/non accentati**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione tra caratteri accentati e non accentati. L'opzione**Distinzione caratteri accentati/non accentati** indica se per i dati viene applicata la distinzione tra caratteri accentati e non accentati e può essere impostata su **True**, **False**o **Auto**. Il valore predefinito **Auto** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione tra caratteri accentati e non accentati, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione Kana**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione dei caratteri Kana. Questa opzione indica se per i dati viene applicata la distinzione dei caratteri Kana e può essere impostata su **True**, **False**o **Auto**. Il valore predefinito **Auto** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione dei caratteri Kana, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione larghezza**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione della larghezza. Questa opzione indica se per i dati viene applicata la distinzione della larghezza e può essere impostata su **True**, **False**o **Auto**. Il valore predefinito **Auto** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione della larghezza, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Interpretare i subtotali come righe di dettaglio**  
 Selezionare un valore per indicare se si desidera che le righe di subtotali vengano interpretate come righe di dettaglio anziché come righe di aggregazione. Il valore predefinito **automatica**, indica che le righe di subtotali devono essere considerate le righe di dettaglio se il report non utilizza il `Aggregate`funzione () per accedere ai campi nel set di dati. Se si vuole che le righe di subtotali vengano interpretate come righe di aggregazione, scegliere **False**. Se si desidera che le righe di subtotali vengano interpretati come righe di dettaglio e si è certi che non usano i `Aggregate`() di funzione, scegliere **True**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le impostazioni locali per un Report o una casella di testo &#40;Reporting Services&#41;](report-design/set-the-locale-for-a-report-or-text-box-reporting-services.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Funzione di aggregazione &#40;Report e SSRS&#41;](report-design/report-builder-functions-aggregate-function.md)  
  
  
