---
description: Funzioni VBA in MDX e DAX
title: Funzioni VBA in MDX e DAX | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dcbf0f0321ddc0c1959c4681c0b1dddf49c1aba
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192291"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funzioni VBA in MDX e DAX


  Questo documento contiene un riferimento incrociato di tutte le funzioni VBA disponibili nelle [funzioni Visual Basic, Applications Edition](/office/vba/Language/Reference/functions-visual-basic-for-applications) supportate in MDX. Inoltre, l'elenco include una nota in caso di equivalenza funzionale con il linguaggio DAX.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Riferimenti a funzioni di Visual Basic, Applications Edition  
  
|Nome funzione|Supportato|Note|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Array|Non supportato||  
|Asc|Solo MDX||  
|AscW|Solo MDX||  
|Atn|Solo MDX||  
|CallByName|Non supportato||  
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
|CLngLng|Non supportato||  
|CLngPtr|Non supportato||  
|Comando|Non supportato||  
|Cos|Solo MDX||  
|CreateObject|Non supportato||  
|CSng|Solo MDX||  
|CStr|Solo MDX||  
|CurDir|Non supportato||  
|CVar|Solo MDX||  
|CVErr|Non supportato||  
|Data|Solo MDX|**Avviso** di DAX implementa una funzione diversa con lo stesso nome; funzione DATE (Year, month, Day), utilizzata per generare un valore di tipo data dagli argomenti specificati.|  
|DateAdd|Solo MDX|**Avviso** di DAX implementa una funzione diversa con lo stesso nome; funzione DATEADD ( \<dates> , <number_of_intervals>, \<interval> ), utilizzata per spostare le date specificate in base a un numero di intervalli specificati|  
|DateDiff|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue|DAX, MDX||  
|Giorno|DAX, MDX||  
|DDB|Solo MDX||  
|Dir|Non supportato||  
|DoEvents|Non supportato||  
|Environ|Non supportato||  
|EOF|Non supportato||  
|Errore|Non supportato||  
|Exp|DAX, MDX||  
|FileAttr|Non supportato||  
|FileDateTime|Non supportato||  
|FileLen|Non supportato||  
|Filtro|Non supportato|**Avviso** di MDX implementa una funzione diversa con lo stesso nome; la funzione FILTER (Set_Expression, Logical_Expression) restituisce il set risultante dall'applicazione di un filtro a un set specificato in base a una condizione di ricerca dagli argomenti specificati.<br /><br /> **Avviso** di DAX implementa una funzione diversa con lo stesso nome; la funzione FILTER ( \<table> , \<filter> ) restituisce una tabella che rappresenta un subset di un'altra tabella o espressione degli argomenti specificati.|  
|Fix|Solo MDX||  
|Format (Visual Basic, Applications Edition)|DAX, MDX||  
|FormatCurrency|Non supportato||  
|FormatDateTime|Non supportato||  
|FormatNumber|Non supportato||  
|FormatPercent|Non supportato||  
|FreeFile|Non supportato||  
|FV|Solo MDX||  
|GetAllSettings|Non supportato||  
|GetAttr|Non supportato||  
|GetObject|Non supportato||  
|GetSetting|Non supportato||  
|Hex|Solo MDX||  
|Ora|DAX, MDX||  
|Iif|Solo MDX|**Avviso** di DAX implementa una funzione simile con il nome: IF (logical_test, value_if_true, value_if_false).|  
|IMEStatus|Non supportato||  
|Input|Non supportato||  
|InputBox|Non supportato||  
|InStr|Solo MDX||  
|InStrRev|Non supportato||  
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
|IsObject|Non supportato||  
|Join|Non supportato||  
|LBound|Non supportato||  
|LCase|Solo MDX||  
|Sinistra|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Non supportato||  
|LOF|Non supportato||  
|File di log|Solo MDX|**Importante** DAX implementa una funzione diversa con lo stesso nome; funzione LOG (Number, base). Viene restituito il logaritmo di un numero nella base specificata dagli argomenti specificati.|  
|LTrim|Solo MDX||  
|MacID|Non supportato||  
|MacScript|Non supportato||  
|Mid|DAX, MDX||  
|Minuto|DAX, MDX||  
|MIRR|Solo MDX||  
|Month|DAX, MDX||  
|MonthName|Non supportato||  
|MsgBox|Non supportato||  
|Adesso|DAX, MDX||  
|NPer|Solo MDX||  
|NPV|Solo MDX||  
|Oct|Solo MDX||  
|Partition|Solo MDX||  
|Pmt|Solo MDX||  
|PPmt|Solo MDX||  
|PV|Solo MDX||  
|QBColor|Solo MDX||  
|Tariffa|Solo MDX||  
|Sostituisci|Non supportato||  
|RGB|Solo MDX||  
|Destra|DAX, MDX||  
|Rnd|Solo MDX||  
|Round|DAX, MDX||  
|RTrim|Solo MDX||  
|Second|DAX, MDX||  
|Seek|Non supportato||  
|Sgn|DAX, MDX||  
|Shell|Non supportato||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Space|Solo MDX||  
|Spc|Non supportato||  
|Doppia visualizzazione|Non supportato||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|string|Solo MDX||  
|StrReverse|Non supportato||  
|Opzione|Solo MDX||  
|SYD|Solo MDX||  
|Scheda|Non supportato||  
|Tan|Solo MDX||  
|Ora|Non supportato||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Taglio|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|Non supportato||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|Non supportato||  
|Giorno della settimana|DAX, MDX||  
|WeekdayName|Non supportato||  
|Year|DAX, MDX||  
  
