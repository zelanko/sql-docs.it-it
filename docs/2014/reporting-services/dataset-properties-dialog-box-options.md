---
title: Finestra di dialogo Proprietà set di dati, opzioni | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10130"
- sql12.rtp.rptdesigner.datasetproperties.options.f1
ms.assetid: 95299049-71ba-427f-b723-775cb696243f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 778365e8fc7f40700b0f8c1683260f15c860a32a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109404"
---
# <a name="dataset-properties-dialog-box-options"></a>Finestra di dialogo Proprietà set di dati, Opzioni
  Selezionare **Opzioni** nella finestra di dialogo **Proprietàset** per modificare le opzioni dei dati, ad esempio le opzioni per le regole di confronto e i subtotali, per la query. Per altre informazioni, vedere [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="options"></a>Opzioni  
 **Regole di confronto**  
 Consente di selezionare le impostazioni locali che determinano la sequenza di regole di confronto da utilizzare per l'ordinamento dei dati. Il valore**Default** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se non è possibile recuperare il valore, il valore predefinito viene ottenuto in base alle impostazioni locali del computer.  
  
 **Distinzione maiuscole/minuscole**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione tra maiuscole e minuscole. Questa opzione indica se per i dati viene applicata la distinzione tra maiuscole e minuscole. È possibile impostare la **distinzione tra maiuscole e minuscole** su **true**, **false**o **auto**. Il valore predefinito **auto**indica che il server di report deve tentare di derivare il valore dal provider di dati durante l'esecuzione del report. Se il provider di dati non supporta il tipo di distinzione tra maiuscole e minuscole, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione caratteri accentati/non accentati**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione tra caratteri accentati e non accentati. Distinzione tra **caratteri accentati** indica se i dati sono sensibili alla distinzione tra caratteri accentati e possono essere impostati su **true**, **false**o **auto**. Il valore predefinito **auto**indica che il server di report deve tentare di derivare il valore dal provider di dati quando il report viene eseguito. Se il provider di dati non supporta il tipo di distinzione tra caratteri accentati e non accentati, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione Kana**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione dei caratteri Kana. Questa opzione indica se i dati sono distinzione Kana sensibili; può essere impostato su **true**, **false**o **auto**. Il valore predefinito **auto**indica che il server di report deve tentare di derivare il valore dal provider di dati durante l'esecuzione del report. Se il provider di dati non supporta il tipo di distinzione dei caratteri Kana, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione larghezza**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione della larghezza. Questa opzione indica se i dati sono con distinzione larghezza e possono essere impostati su **true**, **false**o **auto**. Il valore predefinito **auto**indica che il server di report deve tentare di derivare il valore dal provider di dati durante l'esecuzione del report. Se il provider di dati non supporta il tipo di distinzione della larghezza, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Interpretare i subtotali come righe di dettaglio**  
 Selezionare un valore per indicare se si desidera che le righe di subtotali vengano interpretate come righe di dettaglio anziché come righe di aggregazione. Il valore predefinito, **auto**, indica che le righe di subtotali devono essere considerate come righe di dettaglio se il report non utilizza `Aggregate`la funzione () per accedere ai campi del set di dati. Se si vuole che le righe di subtotali vengano interpretate come righe di aggregazione, scegliere **False**. Se si desidera che le righe di subtotali vengano interpretate come righe di dettaglio e si è certi che non `Aggregate`utilizzino la funzione (), scegliere **true**.  
  
## <a name="see-also"></a>Vedi anche  
 [Impostazione delle impostazioni locali per un report o una casella di testo &#40;Reporting Services&#41;](report-design/set-the-locale-for-a-report-or-text-box-reporting-services.md)   
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Funzione di aggregazione &#40;Generatore report e SSRS&#41;](report-design/report-builder-functions-aggregate-function.md)  
  
  
