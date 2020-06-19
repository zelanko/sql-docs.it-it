---
title: TOKEN (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 43381593b6a43f9e912088a67d5e10401ef3fc6c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969001"
---
# <a name="token--ssis-expression"></a>TOKEN (espressione SSIS)
  Restituisce un token (sottostringa) da una stringa in base ai delimitatori specificati che separano i token nella stringa e al numero del token che indica quale token deve essere restituito.  
  
## <a name="syntax"></a>Sintassi  
  
```  
TOKEN(character_expression, delimiter_string, occurrence)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Stringa che contiene token separati da delimitatori.  
  
 *delimiter_string*  
 Stringa che contiene caratteri delimitatori. Ad esempio, "; ," contiene i caratteri delimitatori punto e virgola, spazio e virgola.  
  
 *occurrence*  
 Intero con segno o senza segno che specifica il token da restituire. Ad esempio, se si specifica 3 come valore per questo parametro, viene restituito il terzo token nella stringa.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_WSTR  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione suddivide il <character_expression> stringa in un set di token separati dai delimitatori specificati nel <delimiter_string> e quindi restituisce l'ennesimo token dove N è il numero di occorrenze del token specificato dal \<occurrence> parametro. Per utilizzi di esempio di questa funzione, vedere la sezione Esempi.  
  
 Le osservazioni seguenti riguardano la funzione TOKEN:  
  
-   La stringa di delimitazione può contenere uno o più caratteri delimitatori.  
  
-   Se il valore del \<occurrence> parametro è maggiore del numero totale di token nella stringa, la funzione restituisce null.  
  
-   I delimitatori iniziali vengono ignorati.  
  
-   La funzione TOKEN può essere utilizzata solo con il tipo di dati DT_WSTR. Se l'argomento *character_expression* è un valore letterale stringa o una colonna di dati con tipo di dati DT_STR, prima di eseguire l'operazione prevista da TOKEN verrà eseguito il cast implicito al tipo di dati DT_WSTR. Per gli altri tipi di dati è necessario il cast esplicito al tipo di dati DT_WSTR.  
  
-   TOKEN restituisce un risultato Null se character_expression è Null.  
  
-   È possibile utilizzare variabili e colonne come valori di tutti gli argomenti dell'espressione.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 Nell'esempio seguente la funzione TOKEN restituisce "a". La stringa "a little white dog" contiene 4 token ("a", "little", "white", "dog") separati dal delimitatore " " (spazio). Il secondo argomento, una stringa delimitatore, specifica il solo delimitatore, lo spazio, da utilizzare per suddividere la stringa di input in token. L'ultimo argomento, 1, specifica che deve essere restituito il primo token. In questa stringa di esempio, il primo token è "a".  
  
```  
TOKEN("a little white dog"," ",1)  
```  
  
 Nell'esempio seguente la funzione TOKEN restituisce "dog". In questo esempio la stringa di delimitazione contiene 5 delimitatori. La stringa di input contiene 4 token: "a", "little", "white", "dog".  
  
```  
TOKEN("a:little|white dog","| ,.:",4)  
```  
  
 Nell'esempio seguente la funzione TOKEN restituisce"" (una stringa vuota) perché non ci sono 99 token nella stringa.  
  
```  
TOKEN("a little white dog"," ",99)  
```  
  
 Nell'esempio seguente la funzione TOKEN restituisce l'intera stringa. La funziona cerca i delimitatori nella stringa di input e poiché non ve ne sono, aggiunge l'intera stringa come primo token.  
  
```  
TOKEN("a little white dog","|",1)  
```  
  
 Nell'esempio seguente la funzione TOKEN restituisce "a". Tutti gli spazi iniziali vengono ignorati.  
  
```  
TOKEN("        a little white dog", " ", 1)  
```  
  
 Nell'esempio seguente la funzione TOKEN restituisce l'anno da una stringa di data.  
  
```  
TOKEN("2009/01/01", "/"), 1  
```  
  
 Nell'esempio seguente la funzione TOKEN restituisce il nome file dal percorso specificato. Se il valore di User::Path è "c:\programmi\data\myfile.txt", ad esempio, la funzione TOKEN restituisce "myfile.txt". La funzione TOKENCOUNT restituisce 4, mentre la funzione TOKEN restituisce il quarto token, "myfile.txt".  
  
```  
TOKEN(@[User::Path], "\\", TOKENCOUNT(@[User::Path], "\\"))  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
