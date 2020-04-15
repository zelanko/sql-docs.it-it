---
title: ALT TABLE - Comando SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304712"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE (comando SQL)
Modifica a livello di codice la struttura di una tabella.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>Argomenti  
 *NomeTabella1*  
 Specifica il nome della tabella la cui struttura viene modificata.  
  
 ADD [COLONNA] *NomeCampo1*  
 Specifica il nome del campo da aggiungere.  
  
 ALTER [COLONNA] *NomeCampo1*  
 Specifica il nome di un campo esistente da modificare.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Specifica il tipo di campo, la larghezza del campo e la precisione del campo (numero di posizioni decimali) per un campo nuovo o modificato.  
  
 *FieldType* è una singola lettera che indica il [tipo di dati](../../odbc/microsoft/visual-foxpro-field-data-types.md)del campo. Alcuni tipi di dati di campo richiedono l'immissione di *nFieldWidth* o *nPrecision* o entrambi.  
  
 *nFieldWidth* e *nPrecision* vengono ignorati per i tipi D, G, I, L, M, P, T e Y. Per impostazione predefinita, *nPrecision* è zero (senza cifre decimali) se *nPrecision* non è incluso per i tipi B, F o N.  
  
 NULL &#124; NOT NULL  
 Consente o impedisce valori Null nel campo.  
  
 Se si omette NULL e NOT NULL, l'impostazione corrente di SET NULL determina se i valori Null sono consentiti nel campo. Tuttavia, se si omette NULL e NOT NULL e si include la clausola PRIMARY KEY o UNIQUE, l'impostazione corrente di SET NULL viene ignorata e il campo non è NULL per impostazione predefinita.  
  
 CHECK *lExpression1*  
 Specifica una regola di convalida per il campo. *lExpression1* deve restituire un'espressione logica e può essere una funzione definita dall'utente o una stored procedure. Ogni volta che viene aggiunto un record vuoto, viene controllata la regola di convalida. Se la regola di convalida non consente un valore di campo vuoto in un record accodato, viene generato un errore.  
  
 ERRORE *cMessageText1*  
 Specifica il messaggio di errore visualizzato quando la regola di convalida del campo genera un errore.  
  
 DEFAULT *eExpression1*  
 Specifica un valore predefinito per il campo. Il tipo di dati di *eExpression1* deve essere lo stesso del tipo di dati per il campo.  
  
 PRIMARY KEY  
 Crea un tag di indice primario. Il tag di indice ha lo stesso nome del campo.  
  
 UNIQUE  
 Crea un tag di indice candidato con lo stesso nome del campo.  
  
> [!NOTE]  
>  Gli indici candidati (creati includendo l'opzione UNIQUE, fornita per la compatibilità ANSI in ALTER TABLE o CREATE TABLE) differiscono dagli indici creati utilizzando l'opzione UNIQUE nel comando INDEX. Un indice creato utilizzando UNIQUE nel comando INDEX consente chiavi di indice duplicate; gli indici candidati non consentono chiavi di indice duplicate.  
  
 I valori Null e i record duplicati non sono consentiti in un campo utilizzato per un indice primario o candidato.  
  
 Se si crea un nuovo campo utilizzando ADD COLUMN, Visual FoxPro non genererà un errore se si crea un indice primario o candidato per un campo che supporta valori Null. Tuttavia, Visual FoxPro genererà un errore se si tenta di immettere un valore null o duplicato in un campo utilizzato per un indice primario o candidato.  
  
 Se si modifica un campo esistente e l'espressione di indice primaria o candidata è costituita da campi nella tabella, Visual FoxPro controlla i campi per verificare se contengono valori null o record duplicati. In caso affermativo, Visual FoxPro genera un errore e la tabella non viene modificata.  
  
 REFERENCES *NomeTabella2* Tag *NomeTag TAG1*  
 Specifica la tabella padre in cui viene stabilita una relazione permanente. TAG *TagName1* specifica il tag di indice della tabella padre su cui si basa la relazione. I nomi dei tag di indice possono contenere fino a 10 caratteri.  
  
 NOCPTRANS  
 Impedisce la conversione in una tabella codici diversa per i campi carattere e memo. Se la tabella viene convertita in un'altra tabella codici, i campi per i quali è stato specificato NOCPTRANS non vengono convertiti. NOCPTRANS può essere specificato solo per i campi carattere e memo.  
  
 Nell'esempio seguente viene creata una tabella denominata mytable che contiene due campi carattere e due campi memo. Il secondo campo carattere, char2, e il secondo campo memo, memo2, includono NOCPTRANS per impedire la conversione.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLONNA] *NomeCampo2*  
 Specifica il nome di un campo esistente da modificare.  
  
 SET DEFAULT *eExpression2*  
 Specifica un nuovo valore predefinito per un campo esistente. Il tipo di dati di *eExpression2* deve essere lo stesso del tipo di dati per il campo.  
  
 SET CHECK *lExpression2*  
 Specifica una nuova regola di convalida per un campo esistente. *lExpression2* deve restituire un'espressione logica e può essere una funzione definita dall'utente o una stored procedure.  
  
 ERRORE *cMessageText2*  
 Specifica il messaggio di errore visualizzato quando la regola di convalida del campo genera un errore. Il messaggio viene visualizzato solo quando i dati vengono modificati all'interno di una finestra Sfoglia o Modifica.  
  
 DROP DEFAULT  
 Rimuove il valore predefinito per un campo esistente.  
  
 CONTROLLO DI RILASCIO  
 Rimuove la regola di convalida per un campo esistente.  
  
 DROP [COLONNA] *NomeCampo3*  
 Specifica un campo da rimuovere dalla tabella. La rimozione di un campo dalla tabella comporta anche la rimozione dell'impostazione del valore predefinito e della regola di convalida del campo.  
  
 Se le espressioni di chiave di indice o trigger fanno riferimento al campo, le espressioni diventano non valide quando il campo viene rimosso. In questo caso, non viene generato un errore quando il campo viene rimosso, ma la chiave di indice non valida o le espressioni trigger genereranno errori in fase di esecuzione.  
  
 SET CHECK *lExpression3*  
 Specifica la regola di convalida della tabella. *lExpression3* deve restituire un'espressione logica e può essere una funzione definita dall'utente o una stored procedure.  
  
 ERRORE *cMessageText3*  
 Specifica il messaggio di errore visualizzato quando la regola di convalida della tabella genera un errore. Il messaggio viene visualizzato solo quando i dati vengono modificati all'interno di una finestra Sfoglia o Modifica.  
  
 CONTROLLO DI RILASCIO  
 Rimuove la regola di convalida della tabella.  
  
 ADD PRIMARY KEY *eExpression3*TAG *TagName2*  
 Aggiunge un indice primario alla tabella. *eExpression3* specifica l'espressione di chiave di indice primaria e *TagName2* specifica il nome del tag di indice primario. I nomi dei tag di indice possono contenere fino a 10 caratteri. Se TAG *TagName2* viene omesso e *eExpression3* è un singolo campo, il tag di indice primario ha lo stesso nome del campo specificato in *eExpression3*.  
  
 RILASCIA CHIAVE PRIMARIA  
 Rimuove l'indice primario e il relativo tag di indice. Poiché una tabella può avere una sola chiave primaria, non è necessario specificare il nome della chiave primaria. La rimozione dell'indice primario comporta anche l'eliminazione di eventuali relazioni persistenti basate sulla chiave primaria.  
  
 ADD UNIQUE *eExpression4*[Tag *TagName3 ]*  
 Aggiunge un indice candidato alla tabella. *eExpression4* specifica l'espressione della chiave di indice candidato e *TagName3* specifica il nome del tag di indice candidato. I nomi dei tag di indice possono contenere fino a 10 caratteri. Se si ospo TAG *TagName3* e *eExpression4* è un singolo campo, il tag di indice candidato ha lo stesso nome del campo specificato in *eExpression4*.  
  
 DROP UNIQUE TAG *TagName4*  
 Rimuove l'indice candidato e il relativo tag di indice. Poiché una tabella può avere più chiavi candidate, è necessario specificare il nome del tag di indice candidato.  
  
 ADD FOREIGN KEY [ *eExpression5*]TAG *TagName4*  
 Aggiunge un indice esterno (non primario) alla tabella. *eExpression5* specifica l'espressione di chiave di indice esterna e *TagName4* specifica il nome del tag di indice esterno. I nomi dei tag di indice possono contenere fino a 10 caratteri.  
  
 REFERENCES *NomeTabella2*[Tag *TagName5*]  
 Specifica la tabella padre in cui viene stabilita una relazione permanente. Includere TAG *TagName5* per stabilire una relazione basata su un tag di indice esistente per la tabella padre. I nomi dei tag di indice possono contenere fino a 10 caratteri. Se si ostrae TAG *TagName5*, la relazione viene stabilita utilizzando il tag di indice primario della tabella padre.  
  
 DROP FOREIGN KEY TAG *TagName6*[SAVE]  
 Elimina una chiave esterna il cui tag di indice è *TagName6*. Se si ostoca SAVE, il tag di indice viene eliminato dall'indice strutturale. Includere SAVE per impedire l'eliminazione del tag di indice dall'indice strutturale.  
  
 RENAME COLUMN *NomeCampo4*a *NomeCampo5*  
 Consente di modificare il nome di un campo della tabella. *NomeCampo4* specifica il nome del campo rinominato. *NomeCampo5* specifica il nuovo nome del campo.  
  
> [!CAUTION]  
>  Prestare attenzione quando si rinominano i campi della tabella perché le espressioni di convalida dei campi e delle tabelle, i comandi e le funzioni possono fare riferimento ai nomi dei campi originali.  
  
 NOVALIDATE  
 Specifica che Visual FoxPro consente di apportare modifiche alla struttura della tabella. queste modifiche potrebbero violare l'integrità dei dati nella tabella. Per impostazione predefinita, Visual FoxPro impedisce ad ALTER TABLE di apportare modifiche che violano l'integrità dei dati nella tabella. Includere NOVALIDATE per eseguire l'override di questo comportamento predefinito.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile utilizzare ALTER TABLE per modificare la struttura di una tabella che non è stata aggiunta a un database. Tuttavia, Visual FoxPro genera un errore se si includono le clausole DEFAULT, FOREIGN KEY, PRIMARY KEY, REFERENCES o SET quando si modifica una tabella libera.  
  
 ALTER TABLE può ricompilare la tabella creando una nuova intestazione di tabella e aggiungendo record all'intestazione della tabella. Ad esempio, la modifica del tipo o della larghezza di un campo potrebbe causare la ricompilazione della tabella.  
  
 Dopo la ricompilazione di una tabella, le regole di convalida dei campi vengono eseguite per tutti i campi il cui tipo o larghezza viene modificato. Se si modifica il tipo o la larghezza di qualsiasi campo della tabella, viene eseguita la regola della tabella.  
  
 Se si modificano le regole di convalida di campi o tabelle per una tabella con record, Visual FoxPro verifica le nuove regole di convalida del campo o della tabella in base ai dati esistenti e genera un avviso alla prima occorrenza di una regola di convalida di un campo o di una tabella o di una violazione del trigger.  
  
 Se la tabella che si modifica si trova in un database, ALTER TABLE - SQL richiede l'utilizzo esclusivo del database. Per aprire un database per l'utilizzo esclusivo, includere EXCLUSIVE in OPEN DATABASE.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TABLE - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX (comando)](../../odbc/microsoft/index-command.md)
