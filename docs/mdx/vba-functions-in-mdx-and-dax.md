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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135016"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funzioni VBA in MDX e DAX


  Questo documento contiene un riferimento incrociato di tutte le funzioni VBA disponibili nella [funzioni di applicazioni Visual Basic](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) che sono supportati in MDX; inoltre, l'elenco include una nota quando si verifica l'equivalenza funzionale con il linguaggio DAX .  
  
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
|Choose|Solo MDX||  
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
|Date|Solo MDX|**Avviso** con DAX viene implementata una funzione diversa con lo stesso nome, cioè la funzione DATE (Year, Month, Day), usato per generare un valore di tipo date dagli argomenti specificati|  
|DateAdd|Solo MDX|**Avviso** DAX viene implementata una funzione diversa con lo stesso nome, il DATEADD (\<date >, < number_of_intervals >,\<interval >) funzione, utilizzato per scorrere le date specificate da un numero di intervalli specificati|  
|DateDiff|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue|DAX, MDX||  
|Day|DAX, MDX||  
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
|Filtro|Non supportate|**Avviso** MDX viene implementata una funzione diversa con lo stesso nome, la funzione FILTER (Set_Expression, Logical_Expression) restituisce il set risultante dal filtraggio di un set specificato in base a una condizione di ricerca dagli argomenti specificati<br /><br /> **Avviso** DAX viene implementata una funzione diversa con lo stesso nome, il filtro (\<tabella >,\<filtro >) funzione restituisce una tabella che rappresenta un subset di un'altra tabella o espressione dagli argomenti specificati|  
|Fix|Solo MDX||  
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
|Iif|Solo MDX|**Avviso** con DAX viene implementata una funzione simile con il nome: IF (logical_test, value_if_true, value_if_false) (funzione).|  
|IMEStatus|Non supportate||  
|Input|Non supportate||  
|InputBox|Non supportate||  
|InStr|Solo MDX||  
|InStrRev|Non supportate||  
|Int|DAX, MDX||  
|IPmt|Solo MDX||  
|IRR|Solo MDX||  
|IsArray|Solo MDX||  
|IsDateMDX solo||  
|IsEmpty|Solo MDX||  
|IsError|DAX, MDX||  
|IsMissing|Solo MDX||  
|IsNull|Solo MDX||  
|IsNumeric|Solo MDX||  
|IsObject|Non supportate||  
|Unisci|Non supportate||  
|LBound|Non supportate||  
|LCase|Solo MDX||  
|Left|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Non supportate||  
|LOF|Non supportate||  
|Log|Solo MDX|**Importante** con DAX viene implementata una funzione diversa con lo stesso nome, la funzione LOG (number, base). Viene restituito il logaritmo di un numero nella base specificata dagli argomenti specificati.|  
|LTrim|Solo MDX||  
|MacID|Non supportate||  
|MacScript|Non supportate||  
|Mid|DAX, MDX||  
|Minuto|DAX, MDX||  
|MIRR|Solo MDX||  
|Mese|DAX, MDX||  
|MonthName|Non supportate||  
|MsgBox|Non supportate||  
|Adesso|DAX, MDX||  
|NPer|Solo MDX||  
|NPV|Solo MDX||  
|Oct|Solo MDX||  
|Partition|Solo MDX||  
|Pmt|Solo MDX||  
|PPmt|Solo MDX||  
|PV|Solo MDX||  
|QBColor|Solo MDX||  
|replica|Solo MDX||  
|Sostituisci|Non supportate||  
|RGB|Solo MDX||  
|Right|DAX, MDX||  
|Rnd|Solo MDX||  
|Arrotondamento|DAX, MDX||  
|RTrim|Solo MDX||  
|Secondo|DAX, MDX||  
|Seek|Non supportate||  
|Sgn|DAX, MDX||  
|Shell|Non supportate||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Spazio|Solo MDX||  
|Spc|Non supportate||  
|divisione|Non supportate||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|String|Solo MDX||  
|StrReverse|Non supportate||  
|Opzione|Solo MDX||  
|SYD|Solo MDX||  
|Scheda|Non supportate||  
|Tan|Solo MDX||  
|Time|Non supportate||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|Non supportate||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|Non supportate||  
|Giorno feriale|DAX, MDX||  
|WeekdayName|Non supportate||  
|Year|DAX, MDX||  
  
  
