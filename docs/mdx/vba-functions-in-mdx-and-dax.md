---
title: Funzioni VBA in MDX e DAX | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 39a0db181f3b1d1a40af1a5fa27ba78366a9d2b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135016"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funzioni VBA in MDX e DAX


  Questo documento contiene un riferimento incrociato di tutte le funzioni VBA disponibili nelle [funzioni Visual Basic, Applications Edition](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) supportate in MDX. Inoltre, l'elenco include una nota in caso di equivalenza funzionale con il linguaggio DAX.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Riferimenti a funzioni di Visual Basic, Applications Edition  
  
|Nome funzione|Supportato|Note|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Array|Non supportate||  
|Asc|Solo MDX||  
|AscW|Solo MDX||  
|Atn|Solo MDX||  
|CallByName|Non supportate||  
|CBool|Solo MDX||  
|CByte|Solo MDX||  
|CCur|Solo MDX||  
|CDate|Solo MDX||  
|CDbl|Solo MDX||  
|CDec|Solo MDX||  
|Scegliere|Solo MDX||  
|Chr|Solo MDX||  
|CInt|Solo MDX||  
|CLng|Solo MDX||  
|CLngLng|Non supportate||  
|CLngPtr|Non supportate||  
|Comando|Non supportate||  
|Cos|Solo MDX||  
|CreateObject|Non supportate||  
|CSng|Solo MDX||  
|CStr|Solo MDX||  
|CurDir|Non supportate||  
|CVar|Solo MDX||  
|CVErr|Non supportate||  
|Data|Solo MDX|**Avviso** di DAX implementa una funzione diversa con lo stesso nome; funzione DATE (Year, month, Day), utilizzata per generare un valore di tipo data dagli argomenti specificati.|  
|DateAdd|Solo MDX|**Avviso** di DAX implementa una funzione diversa con lo stesso nome; funzione DATEADD (\<dates>, <number_of_intervals>\<, Interval>), usata per spostare le date specificate in base a un numero di intervalli specificati|  
|DateDiff|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue|DAX, MDX||  
|Giorno|DAX, MDX||  
|DDB|Solo MDX||  
|Dir|Non supportate||  
|DoEvents|Non supportate||  
|Environ|Non supportate||  
|EOF|Non supportate||  
|Errore|Non supportate||  
|Exp|DAX, MDX||  
|FileAttr|Non supportate||  
|FileDateTime|Non supportate||  
|FileLen|Non supportate||  
|Filtro|Non supportate|**Avviso** di MDX implementa una funzione diversa con lo stesso nome; la funzione FILTER (Set_Expression, Logical_Expression) restituisce il set risultante dall'applicazione di un filtro a un set specificato in base a una condizione di ricerca dagli argomenti specificati.<br /><br /> **Avviso** di DAX implementa una funzione diversa con lo stesso nome; la funzione FILTER\<(Table>\<, Filter>) restituisce una tabella che rappresenta un subset di un'altra tabella o espressione degli argomenti specificati.|  
|Correzione|Solo MDX||  
|Format (Visual Basic, Applications Edition)|DAX, MDX||  
|FormatCurrency|Non supportate||  
|FormatDateTime|Non supportate||  
|FormatNumber|Non supportate||  
|FormatPercent|Non supportate||  
|FreeFile|Non supportate||  
|FV|Solo MDX||  
|GetAllSettings|Non supportate||  
|GetAttr|Non supportate||  
|GetObject|Non supportate||  
|GetSetting|Non supportate||  
|Hex|Solo MDX||  
|Ora|DAX, MDX||  
|Iif|Solo MDX|**Avviso** di DAX implementa una funzione simile con il nome: IF (logical_test, value_if_true, value_if_false).|  
|IMEStatus|Non supportate||  
|Input|Non supportate||  
|InputBox|Non supportate||  
|InStr|Solo MDX||  
|InStrRev|Non supportate||  
|Int|DAX, MDX||  
|IPmt|Solo MDX||  
|IRR|Solo MDX||  
|IsArray|Solo MDX||  
|Solo IsDateMDX||  
|IsEmpty|Solo MDX||  
|IsError|DAX, MDX||  
|IsMissing|Solo MDX||  
|IsNull|Solo MDX||  
|IsNumeric|Solo MDX||  
|IsObject|Non supportate||  
|Join|Non supportate||  
|LBound|Non supportate||  
|LCase|Solo MDX||  
|Left|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Non supportate||  
|LOF|Non supportate||  
|File di log|Solo MDX|**Importante** DAX implementa una funzione diversa con lo stesso nome; funzione LOG (Number, base). Viene restituito il logaritmo di un numero nella base specificata dagli argomenti specificati.|  
|LTrim|Solo MDX||  
|MacID|Non supportate||  
|MacScript|Non supportate||  
|Mid|DAX, MDX||  
|Minuto|DAX, MDX||  
|MIRR|Solo MDX||  
|Month|DAX, MDX||  
|MonthName|Non supportate||  
|MsgBox|Non supportate||  
|Now|DAX, MDX||  
|NPer|Solo MDX||  
|NPV|Solo MDX||  
|ott|Solo MDX||  
|Partition|Solo MDX||  
|Pmt|Solo MDX||  
|PPmt|Solo MDX||  
|PV|Solo MDX||  
|QBColor|Solo MDX||  
|Tariffa|Solo MDX||  
|Replace|Non supportate||  
|RGB|Solo MDX||  
|Right|DAX, MDX||  
|Rnd|Solo MDX||  
|Round|DAX, MDX||  
|RTrim|Solo MDX||  
|Second|DAX, MDX||  
|Seek|Non supportate||  
|Sgn|DAX, MDX||  
|Shell|Non supportate||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Spazio|Solo MDX||  
|Spc|Non supportate||  
|Split|Non supportate||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|string|Solo MDX||  
|StrReverse|Non supportate||  
|Opzione|Solo MDX||  
|SYD|Solo MDX||  
|Scheda|Non supportate||  
|Tan|Solo MDX||  
|Tempo|Non supportate||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|Non supportate||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|Non supportate||  
|Giorno della settimana|DAX, MDX||  
|WeekdayName|Non supportate||  
|Year|DAX, MDX||  
  
  
