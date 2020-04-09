---
title: Risolvere i problemi di elaborazione dei report di Reporting Services
description: In questo articolo vengono risolti i problemi che si verificano quando il componente Elaborazione report combina i dati e le informazioni sul layout e valuta le espressioni di proprietà degli elementi del report.
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1d10dc9e4e5808fbc9c315cb262a1b2136c73029
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664437"
---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>Risolvere i problemi di elaborazione dei report di Reporting Services
Dopo aver recuperato i dati del report, le informazioni sul layout e i dati vengono combinati dal componente Elaborazione report. Ciascuna proprietà dell'elemento del report contenente un'espressione viene valutata nel contesto dei dati e del layout combinati. Utilizzare le informazioni presenti in questo argomento per risolvere questi problemi.   
  
## <a name="my-report-definition-is-not-valid"></a>La definizione del report non è valida.  
In fase di esecuzione, il componente Elaborazione report combina i dati e gli elementi di layout nella definizione del report e valuta le espressioni per le proprietà degli elementi del report.   
  
Il componente Elaborazione report controlla che la definizione del report (file rdl) sia conforme allo schema specificato nella dichiarazione dello spazio dei nomi all'inizio del file rdl. Per altre informazioni sugli schemi RDL, vedere [Individuare la versione dello schema di definizione del report (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
Inoltre, le espressioni del report valutate in fase di esecuzione devono seguire un set di regole che assicurano che i dati del report e il layout vengano combinati correttamente. Quando il componente Elaborazione report rileva un problema, è possibile che venga visualizzato il messaggio seguente: La definizione del report `<report name>` è non valida.  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>Le espressioni per gli elementi dei report possono fare riferimento solo ai campi inclusi nell'ambito del set di dati corrente oppure, se contenute in una funzione di aggregazione, a campi inclusi nell'ambito del set di dati specificato."  
  
Utilizzare l'elenco seguente per determinare la causa dell'errore:  
* Quando un report dispone di più di un set di dati, è necessario che un parametro di ambito sia specificato in un'espressione di aggregazione in una casella di testo nel corpo del report, Ad esempio: `=First(Fields!FieldName.Value, "DataSet1")`.  
  
Per specificare un parametro di ambito, fornire il nome di un set di dati, un'area dati o un gruppo che è compreso nell'ambito per l'elemento del report. Per altre informazioni, vedere [Informazioni sull'ambito di espressioni per totali, aggregazioni e raccolte predefinite (Generatore report 3.0 e SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) e [Riferimento alle espressioni (Generatore report 3.0 e SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md).  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>I nomi degli oggetti devono contenere un numero di caratteri maggiore o uguale a 0 e minore o uguale a 256.  
La lunghezza degli identificatori di oggetti in una definizione di report è limitata a 256 caratteri. Gli identificatori devono prevedere la distinzione tra maiuscole e minuscole ed essere conformi a CLS. I nomi devono iniziare con una lettera e contenere lettere, numeri e un carattere di sottolineatura (_). Non deve essere presente alcuno spazio. Ad esempio, i nomi delle caselle di testo o i nomi delle aree dati devono essere conformi a queste linee guida.   
  
Per modificare il nome di un oggetto, sulla barra degli strumenti del riquadro Proprietà selezionare l'elemento nell'elenco a discesa, scorrere fino a **Nome** e immettere un nome di oggetto valido.   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>Viene visualizzata una casella di testo "#Errore".  
Il messaggio "#Errore" si verifica quando il componente Elaborazione report valuta le espressioni nelle proprietà degli elementi del report in fase di esecuzione e rileva un errore di conversione del tipo di dati, dell'ambito o di altro genere.   
  
Un errore del tipo di dati di solito indica che il tipo di dati specificato o predefinito non è supportato. Un errore dell'ambito indica che l'ambito specificato non è disponibile al momento della valutazione dell'espressione.   
  
Per eliminare il messaggio #Errore, è necessario riscrivere l'espressione che lo ha causato. Per ulteriori informazioni sul problema, visualizzare il messaggio di errore dettagliato.   
  
Nell'anteprima, visualizzare la finestra di output in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)]. Nel server di report, visualizzare lo stack di chiamate. 
  
  
## <a name="see-also"></a>Vedere anche  
[Errori ed eventi (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

