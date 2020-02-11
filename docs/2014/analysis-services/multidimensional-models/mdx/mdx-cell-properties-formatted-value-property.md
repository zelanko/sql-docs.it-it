---
title: LINGUA e FORMAT_STRING FORMATED_VALUE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a116be708dd714a48d1cc936a08350237ca98ddf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074402"
---
# <a name="language-and-format_string-on-formated_value"></a>LANGUAGE e FORMAT_STRING in FORMATED_VALUE
  La proprietà FORMATTED_VALUE è compilata in base alle interazioni delle proprietà VALUE, FORMAT_STRING e LANGUAGE della cella. In questo argomento viene illustrato come interagiscono queste proprietà per compilare la proprietà FORMATTED_VALUE.  
  
## <a name="value-format_string-language-properties"></a>Proprietà VALUE, FORMAT_STRING e LANGUAGE  
 Nella tabella seguente vengono descritte queste proprietà e viene illustrato come utilizzarle insieme.  
  
 VALORE  
 Valore non formattato della cella.  
  
 FORMAT_STRING  
 Modello di formattazione da applicare al valore della cella per generare la proprietà FORMATTED_VALUE  
  
 LANGUAGE  
 Specifica delle impostazioni locali da applicare insieme a FORMAT_STRING per generare una versione localizzata di FORMATTED_VALUE  
  
## <a name="formatted_value-constructed"></a>Proprietà FORMATTED_VALUE costruita  
 La proprietà FORMATTED_VALUE viene costruita utilizzando il valore della proprietà VALUE e applicando a tale valore il modello di formato specificato nella proprietà FORMAT_STRING. Inoltre, ogni volta che il valore di formattazione è dato da un `named formatting literal`, la specifica della proprietà LANGUAGE modifica l'output di FORMAT_STRING per seguire l'utilizzo della lingua per la formattazione denominata. I valori letterali di formattazione denominati sono tutti definiti in modo da poter essere localizzati. Contrariamente al modello `"General Date"` che indica che la data deve essere presentata come definita dal modello indipendentemente dalla specifica della lingua, la specifica `"YYYY-MM-DD hh:nn:ss",` può essere localizzata.  
  
 Se si verifica un conflitto tra il modello FORMAT_STRING e la specifica LANGUAGE, il modello FORMAT_STRING esegue l'override della specifica LANGUAGE. Se, ad esempio, FORMAT_STRING="$ #0", LANGUAGE=1034 (Spagna) e VALUE=123.456, allora FORMATTED_VALUE="$ 123" anziché FORMATTED_VALUE="€ 123". Il formato previsto è in euro perché il valore del modello di formato esegue l'override della lingua specificata.  
  
### <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato l'output ottenuto quando la proprietà LANGUAGE viene utilizzata insieme a FORMAT_STRING.  
  
 Nel primo esempio vengono illustrati i valori numerici di formattazione, nel secondo vengono illustrati i valori data e ora di formattazione.  
  
 Per ogni esempio viene specificato il codice MDX (Multidimensional Expressions).  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Di seguito sono riportati i risultati trasposti ottenuti eseguendo la query MDX indicata in precedenza usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] in un server e un client con l'impostazione locale 1033:  
  
|Membro|FORMATTED_VALUE|Spiegazione|  
|------------|----------------------|-----------------|  
|Una|$5,040.00|La proprietà FORMAT_STRING è impostata su `Currency` e la proprietà LANGUAGE su `1033`, valore ereditato dalle impostazioni locali del sistema|  
|b|€ 5.040,00|La proprietà FORMAT_STRING è impostata su `Currency` (valore ereditato da A) e la proprietà LANGUAGE è impostata in modo esplicito su `1034` (Spagna), da qui il simbolo dell'euro e i separatori decimale e delle migliaia diversi.|  
|C|$5.040,00|La proprietà FORMAT_STRING è impostata su `$#,##0.00` un override di Currency, da A, e la proprietà LANGUAGE è impostata in modo esplicito su `1034` (Spagna). Poiché la proprietà FORMAT_STRING ha impostato in modo esplicito il simbolo di valuta su $, la proprietà FORMATTED_VALUE viene presentata con il simbolo $. Tuttavia, poiché `.` (punto) e `,` (virgola) sono rispettivamente segnaposto per il separatore decimale e il separatore delle migliaia, la specifica della lingua influisce su di essi generando un output localizzato per i separatori decimali e delle migliaia.|  
|D|5.04E+03|La proprietà FORMAT_STRING è impostata su `Scientific` e la proprietà LANGUAGE su `1033`, valore ereditato dalle impostazioni locali del sistema, da qui il punto ( `.` ) come separatore decimale.|  
|E|5,04E+03|La proprietà FORMAT_STRING è impostata su `Scientific` e la proprietà LANGUAGE è impostata in modo esplicito su `1034,` da qui la virgola ( `,` ) come separatore decimale.|  
|F|50.40%|La proprietà FORMAT_STRING è impostata su `Percent` e la proprietà LANGUAGE su `1033`, valore ereditato dalle impostazioni locali del sistema, da qui il punto ( `.` ) come separatore decimale.<br /><br /> Si noti che la proprietà VALUE è stata modificata da 5040 a 0.5040|  
|G|50,40%|La proprietà FORMAT_STRING è impostata su `Percent`, valore ereditato da F, e la proprietà LANGUAGE è impostata in modo esplicito su `1034` , da qui la virgola ( `,` ) come separatore decimale.<br /><br /> Si noti che la proprietà VALUE è stata ereditata da F.|  
|H|No|La proprietà FORMAT_STRING è impostata su `YES/NO`, la proprietà VALUE su 0 e la proprietà LANGUAGE è impostata in modo esplicito su `1034`. Poiché non vi è differenza tra il NO inglese e quello spagnolo, l'utente non nota alcuna differenza nella proprietà FORMATTED_VALUE.|  
|I|SI|La proprietà FORMAT_STRING è impostata su `YES/NO`, la proprietà VALUE su 59 e la proprietà LANGUAGE è impostata in modo esplicito su `1034`. Come definito per la formattazione YES/NO, qualsiasi valore diverso da zero (0) è un YES e poiché la lingua è impostata sullo spagnolo, la proprietà FORMATTED_VALUE è SI.|  
|J|Desactivado|La proprietà FORMAT_STRING è impostata su `ON/OFF`, la proprietà VALUE su 0 e la proprietà LANGUAGE è impostata in modo esplicito su `1034`. Come definito per la formattazione ON/OFF, qualsiasi valore uguale a zero (0) è un OFF e poiché la lingua è impostata sullo spagnolo, la proprietà FORMATTED_VALUE è Desactivado.|  
|K|Activado|La proprietà FORMAT_STRING è impostata su `ON/OFF`, la proprietà VALUE su -312 e la proprietà LANGUAGE è impostata in modo esplicito su `1034`. Come definito per la formattazione ON/OFF, qualsiasi valore diverso da zero (0) è un ON e poiché la lingua è impostata sullo spagnolo, la proprietà FORMATTED_VALUE è Activado.|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Di seguito sono riportati i risultati trasposti ottenuti eseguendo la query MDX indicata in precedenza usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] in un server e un client con l'impostazione locale 1033:  
  
|Membro|FORMATTED_VALUE|Spiegazione|  
|------------|----------------------|-----------------|  
|Una|3/12/1959 6:30:00 AM|La proprietà FORMAT_STRING è impostata in modo implicito su `General Date` dall'espressione CDate() e la proprietà LANGUAGE è impostata su `1033` (Inglese), valore ereditato dalle impostazioni locali del sistema|  
|b|Thursday, March 12, 1959|La proprietà FORMAT_STRING è impostata in modo esplicito su `Long Date` e la proprietà LANGUAGE è impostata su `1033` (inglese), valore ereditato dalle impostazioni locali del sistema|  
|C|12/03/1959 6:30:00|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `General Date` e `1034` (spagnolo).<br /><br /> Rispetto allo stile di formattazione americano, mese e giorno sono invertiti.|  
|D|jueves, 12 de marzo de 1959|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `Long Date` e `1034` (spagnolo).<br /><br /> In spagnolo mese e giorno della settimana sono riportati per esteso|  
|E|1959/03/12 6:30:00|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `General Date` e `1041` (giapponese).<br /><br /> La data presenta ora il formato anno/mese/giorno ora:minuti:secondi|  
|F|1959年3月12日|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `Long Date` e `1041` (giapponese).|  
|G|6:30:00 AM|La proprietà FORMAT_STRING è impostata in modo esplicito su `Long Time` e la proprietà LANGUAGE è impostata su `1033` (inglese), valore ereditato dalle impostazioni locali del sistema.|  
|H|06:30|La proprietà FORMAT_STRING è impostata in modo esplicito su `Short Time` e la proprietà LANGUAGE è impostata su `1033` (inglese), valore ereditato dalle impostazioni locali del sistema.|  
|I|6:30:00|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `Long Time` e `1034` (spagnolo).|  
|J|06:30|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `Short Time` e `1034` (spagnolo).|  
|K|6:30:00|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `Long Time` e `1041` (giapponese).|  
|L|06:30|Le proprietà FORMAT_STRING e LANGUAGE sono impostate in modo esplicito rispettivamente su `Short Time` e `1041` (giapponese).|  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto FORMAT_STRING &#40;MDX&#41;](mdx-cell-properties-format-string-contents.md)   
 [Utilizzo delle proprietà delle celle &#40;&#41;MDX](mdx-cell-properties-using-cell-properties.md)   
 [Creazione e utilizzo di valori di proprietà &#40;MDX&#41;](../../creating-and-using-property-values-mdx.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
